# GIT versionhallintajärjestelmä

## Mikä on versionhallinta?

Versionhallinnan tarkoituksena on säilyttää koodiin tehdyt muutokset ja mahdollistaa jo muutetun tiedoston palautus aikaisempaan versioon. Versionhallinta mahdollistaa myös tehokkaamman projektin hallinnan tiedostojen jakamisen ollessa helppoa.

## Miten versionhallinta otetaan käyttöön?

Tällä hetkellä versionhallintajärjestelmien suuret nimet ovat GitHub ja GitLab, joista Helsingin yliopisto käyttää omaa GitLab serveriään, version.helsinki.fi.

Aloitettaessa tämän käyttöä, on ensin kirjauduttava version.helsinki.fi palveluun kerran, jotta järjestelmä luo tunnukset palveluun.

## Ohjelmistot

Asennusohjeet eri käyttöjärjestelmille: https://git-scm.com/book/en/v2/Getting-Started-Installing-Git

## Käyttö

Käytännössä yhden henkilön projektissa selviää pitkälti muutamalla käskyllä:

	>>>git clone # Käytetään projektin lataamiseen omalle koneelle

	>>>git status # Kertoo projektin nykyisen tilan

	>>>git add # Lisää version hallinnan piiriin tiedostoja

	>>>git commit # Suorittaa muutoksen varmistuksen, joka myöhemmin siirretään serverille

	>>>git push # Suorittaa "commit" käskyllä tehdyn varmistuksen lataamisen serverille

GITiin ei ole tarkoitus lisätä mitään data-tiedostoja, kuten .csv, .xlsx tai .mat. Tarkoituksena on säilyttää näitä datoja käyttäviä tiedostoja. Datan hallinta pitäisi projektissa suorittaa tietokantapalvelimen tai yhteisen verkkolevyn kautta.

## Esimerkki

1. Mennään version.helsinki.fi sivulle
2. Projektit sivulta pitäisi löytyä create project nappi
   - Jos nappia ei löydy, saatat olla "vieraileva" tunnus, jolla ei ole oikeuksia itse luoda projekteja.
3. Seuraa ohjeita loppuun
4. Yläoikealta pitäisi löytyä nappi *clone*. Kopioi SSH-linkki valikosta.
5. Kirjoita komentoriville:
```bash
git clone <linkki>
```
6. Projektin pitäisi latautua nykyisen kansioon uuteen kansioon.
7. Mennään kansioon sisälle

```bash
cd <kansionimi>
```

8. Tällä hetkellä kansiossa ei pitäisi olla tiedostoja (README.md saattaa löytyä, jos se valittiin projektin luonnin aikana.)
9. Luodaan mikä tahansa tiedosto kantaan. Esimerkiksi Python "Hei maailma!"-ohjelma

```bash
echo "print('Hei maailma!')" >> hello_world.py
```

10. Nyt ```git status``` käskyllä pitäisi näkyä hello_world.py tiedosto versionhallinan piiristä puuttuvana tiedostona.
11. Lisätään se hallinnan piiriin

```bash
git add hello_world.py
```

12. Suoritetaan muutos ja kirjataan kirjausviesti avautuvaan tekstieditoriin.

```bash
git commit
```

13. Lähetetään muutos serverille

```bash
git push
```

Tässä kohtaa saattaa tulla virheitä, jotka valittavat "upstreamin" puutteesta. Tässä vaiheessa näistä ei tarvitse välittää ja gitin tulostamia ohjeita noudattamalla saadaan muutos lähetettyä virheettä serverille.

14. Ensimmäinen GIT projekti on nyt käytössä tietokoneellasi! Onneksi olkoon!

