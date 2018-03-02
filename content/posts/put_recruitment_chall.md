---
title: "PUT - rekrutacja otwarta!"
date: 2018-03-02T22:31:07+01:00
draft: true
---

## We need YOU in... 

... naszym zespole! Jeśli interesujesz się szeroko pojętym `bezpieczeństwem`, lub znudziły Ci się zwykłe hackathony/compo oraz masz ochotę się nie wyspać ;) to dobrze trafiłeś/aś! Nasz CTFowy zespół poszukuje zawodników. W tym celu  postanowiliśmy ogłosić otwarty nabór.

## Ale po kolei!

Dla wszystkich chętnych przygotowaliśmy parę prostych zadań. Dla osób, które parsują nagłówki bitmapy w głowie, zjadły zęby na ROPchainach czy znają na pamięć całą tablicę syscalli Linuxa (coś koło 300 pozycji), poniższe problemy będą trywialne. Jeśli natomiast dopiero zaczynasz z CTFami i właśnie dowiedziałeś/aś się, że na Twojej uczelni działa zespół łapiący flagii, odnalezienie zaszytych informacji, z pewnością dostarczy Tobie dużo frajdy. Przy okazji, zobaczysz jak mniej więcej wygląda rywalizacja w tego typu wydarzeniach. 

Ważna informacja, niemal kluczowa - ułatwiliśmy Wam zadanie, każda flaga ma jednakowy format. Jeśli natkniesz się na ciąg `PUT{tutaj_jakaś_flaga}`, to znaczy, że jesteś w domu! Koniecznie podeślij nam rozwiązanie na naszego maila! `putctf@protonmail.com`

## Ach te nowe technologie

Chcieliśmy spróbować Javy w wersji Script. Niestety, coś poszło nie tak. Wyszedł nam co prawda rozpoznawany przez przeglądarkę kod, natomiast jest on totalnie niezrozumiały! Jesteś w stanie pomóc nam rozwiązać tę zagadkę? Webaplikacje takie trudne...

[wchodzę_w_to!](https://raw.githubusercontent.com/PUT-CTF/put_small_ctf_1/master/1_javascript.js)

## Może tego nie widać na pierwszy rzut oka...

ale ten obrazek, nie jest zwyczajny. Gdzieś tam kryje się flaga, którą trzeba odzyskać. Niestety, zapomnieliśmy jak to się robi... Pomożesz? ;) Wystarczy wypakować zipa i zrobić trochę magii...

[pokażcie_co_tam_macie](https://github.com/PUT-CTF/put_small_ctf_1/blob/master/2_stegano.zip)

## Symboliczne crackme

Kolejną misją, jest crackme. Ten dziwny ciąg znaków pewnie kojarzysz. Dwa `==` podpowiadają, że jest to base64. Piszemy o tym, ponieważ tyle pamiętamy. Możesz zamienić ten tekst na binarkę na przykład w ten sposób: `cat plik_tekstowy.tx | base64 -d > file.bin`. Niestety, autor zadania zgubił gdzieś pasujące hasło. Wystarczy, że je znajdziesz. Wydaje nam się, że było dość długie, także rekrutacja może się skończyć przed sprawdzeniem wszystkich możliwości! 

To zadanie można rozwiązać na wiele sposobów, starczy nam jedno, nawet najprostsze rozwiązanie. Jeśli zaprzęgniesz do tego celu SMT solver albo poszukasz side channel attacku, to wywrzesz na nas jeszcze większe wrażenie, niż rozwiązując je one-linerem!

[pobrałem_debugger_i_hexedytor_dajcie_zadanie!](https://github.com/PUT-CTF/put_small_ctf_1/blob/master/3_crackme_0x001.tar.gz)


## Baw się dobrze!

I pamiętaj, każde zadanie, które uda Ci się rozwiązać, wyślij do nas mailem! Opisy rozwiązań mile widziane! Autorów prosimy jednak o wstrzymanie się z ich publikacją do czasu zamknięcia zgłoszeń, czyli do {}.@hh_wstaw_proszę_datę

Kończy nam się wiaderko Internetu, wracamy niebawem!

Over and out.

