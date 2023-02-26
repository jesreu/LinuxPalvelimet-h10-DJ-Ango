# LinuxPalvelimet-h10-DJ-Ango
    Kirjoittanut: Jesse Reunamo
    Kurssi:       Linux-palvelimet
    Linkki:       https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/

## a)
Luodaan oma tietokantasovellus käyttämällä django kehysympäristöä.

### Kehitysympäristön luominen
Aloitetaan prosessi asentamalla virtualenv paketti, jolla voidaan luoda virtuaalisia python ympäristöjä. Kannattaa myös ajaa komento `man virtualenv` asennuksen jälkeen, jotta voit tutustua työkaluun.

    sudo apt-get -y install virtualenv
    man virtualenv

![Virtualenv](https://user-images.githubusercontent.com/112503770/221422648-8e97f427-cdea-4dc9-9b06-95afeb6e3957.png)


Nyt voimme käyttää asennettua virtualenv ohjelmaa. Voimme ajaa alapuolella olevan komennon, jossa luomme uuden virtuaaliympäristön käyttöömme. Komennon liput: --system-site-packages: mahdollistaa virtuaaliympäristön käyttää ympäristön ulkopuolisia paketteja.  -p lippu määrittää käytetyn python version ja lopussa env/ on sijaintina. 

    virtualenv --system-site-packages -p python3 env/
    
![systemsite](https://user-images.githubusercontent.com/112503770/221422633-8c312bcf-d9ae-4ef9-b81b-b7694496dfee.png)

![p flagi](https://user-images.githubusercontent.com/112503770/221422636-d83a8019-f674-45dd-9afe-7260fa6459a4.png)


Otetaan virtuaaliympäristö käyttöön komennolla:

    source env/bin/activate
    
![virtuaaliymparisto](https://user-images.githubusercontent.com/112503770/221422684-b5a978b6-ded8-4411-9d0e-6e048a9b3fb4.png)

Kuvassa näkyy komentopäätteen vasemmalle ilmestynyt (env), joka tarkoittaa että toimimme virtuaaliympäristössä.

Tarkistaa, että pip asennetaan virtuaaliympäristöön komennolla:

    which pip
    
![pip menee virtuaaliin](https://user-images.githubusercontent.com/112503770/221422736-f58d1401-bd3e-42b6-a0cc-2398e4782412.png)

Kuvasta näkee `/env` kirjaston, joten oikea osoite kyseessä. Kirjoitetaan tekstitiedostoon ohjelmat, jotka haluamme asentaa.

    micro requirements.txt
    
![asennettavat ohjelmat](https://user-images.githubusercontent.com/112503770/221422797-edf291f6-4050-4c3a-a137-543a3730884a.png)
   
Ajamalla komennon asennamme tiedostossa lukevat ohjelmat. Voimme tarkistaa, että django asentui ajamalla --version komennon.

    pip install -r requirements.txt
    django-admin --version
    
![django onnistui ja versio](https://user-images.githubusercontent.com/112503770/221422767-619086f1-5dd1-4afe-b964-26e6df8a8cc8.png)

### Djangon käynnistäminen  
Aloitetaan uusi django projekti (tietokanta/weppisivu) komennoilla:

    django-admin startproject sivuco
    cd sivuco
    
Käynnistetään projekti komennolla:

    ./manage.py runserver
    
![serveripaalle](https://user-images.githubusercontent.com/112503770/221422903-9e2a1039-18c2-4e36-bc8c-2ea3647eb6d0.png)

Voimme vielä kokeilla netissä sivulla `127.0.0.1:8000`, että sivu toimii.

![Onnistunut asennus](https://user-images.githubusercontent.com/112503770/221423730-a99205fc-1639-4427-84de-4dde215bdbc9.png)

 ### Admin käyttäjän luominen
Lopeta severin ajaminen painamalla `ctrl + c`, jotta voimme ajaa komentoja samalla ikkunalla.

Päivitetään tietokanta komennoilla:

    ./manage.py makemigrations
    ./manage.py migrate

Salasanan luomiseen asennetaan pwgen paketti, jolla voimme generoida turvallisen salasanan. Salasana näkyy kuvassa, koska tämä projekti on vain paikallinen, jos kyseessä olisi weppiin menevä projekti niin ei kannata jakaa salasanaa.

    sudo apt-get install pwgen
    pwgen -s 20 1
    
![generoitu salsan](https://user-images.githubusercontent.com/112503770/221422923-6a572ac7-f708-4181-be1e-5a67ae299b32.png)
  
Adminkäyttäjän luominen aja alapuolella oleva komento ja vastaa sen haluamiin kysymyksiin. Käynnistetään sivu myös uudelleen `runserver` komennolla.

    ./manage.py createsuperuser
    ./manage.py runserver
    
Testaan onnistuiku käyttäjän lisääminen menemällä `127.0.0.1:8000/admin/` osoitteeseen ja kirjautumalla sinne.

![kirjautumisen kokeilu](https://user-images.githubusercontent.com/112503770/221422990-ad539c87-7636-40f2-8f8e-ea5a32d9480d.png)

### Toisen käyttäjän luominen

Luodaan toinen käyttäjä webbiliittymän kautta, koska oikealle käyttäjälle ei tulisi antaa admin käyttäjää. Voit lisätä uuden käyttäjän klikkaamalla `+ Add` vaitoehtoa Users kentän oikealla puolella

![uusikäyttäjä](https://user-images.githubusercontent.com/112503770/221423841-c448e607-791a-4a8c-bb8b-d34b21559d03.png)

Sivu kysyy käyttäjän nimen, salasanan ja muut tiedot. Täytä ne hyvän tietoturvan mukaisesti. Kun olet tehnyt uuden käyttäjän, voit muokata käyttäjän oikeuksia klikkaamalla `Users` kenttää, joka avaa sivun missä näet kaikki käyttäjät.

![Kayttajat](https://user-images.githubusercontent.com/112503770/221423045-ceff6bdf-d15b-4c75-bdeb-49e1965f6773.png)

Klikkaamalla lisäämäsi käyttäjää, (minun tapauksessa EssiEsimerkki) aukeaa sivu, jossa voit asettaa käyttäjälle tarvittavat oikeudet. 

![oikeudet](https://user-images.githubusercontent.com/112503770/221423022-8e106238-9a92-44d8-bec8-6f16e11e3170.png)

Nyt voit kirjautua ulos admin käyttäjältä ja vaihtaa normaalille käyttäjälle.

### Tietokannan luominen b)
Luodaan kansio crm (customer relational management) applikaatiolle

    ./manage.py startapp crm
    
    micro sivuco/settings.py
    
![uusi applikaatio](https://user-images.githubusercontent.com/112503770/221423064-3e4c8768-4214-4fa3-ada6-e5e2e2f6772f.png)

Muokataan models.py tiedostoa, jossa voimme määrittää tietokannan luokkia, tässä tapauksessa on Oppilas, jolla voi olla useita Arvosanoja.
    micro crm/models.py

![tietokannan tierot](https://user-images.githubusercontent.com/112503770/221423158-6f8f3005-c2d2-4ce0-8050-97cfd2771d01.png)

Ajetaan komennot:

    ./manage.py makemigrations
    ./manage.py migrate
    
Ajatessa ilmeni virhe:

![virhe](https://user-images.githubusercontent.com/112503770/221423076-841735c5-9c78-4004-8a29-971a2e16728c.png)

Oletan, että kyseessä on kirjoitusvirhe, joten ajan kommennon `micro crm/models.py` ja korjaan kuvassa näkyvän ison L kirjaimen. Ajan uudelleen komennot:
    
    ./manage.py makemigrations
    ./manage.py migrate

Rekisteröidään admin sivulle tehdyt modelit, jotta ne näkyvät weppisivulla.

    micro crm/admin.py
    
kuve![rekisterointi](https://user-images.githubusercontent.com/112503770/221423122-a12035dd-36c5-4cf6-9493-c8aa3ec9c99b.png)


Käynnistetään serveri vielä, jotta voidaan tarkistaa tulivatko luokat näkyviin.
    
    ./manage.py runserver
    
![luokat näkyy](https://user-images.githubusercontent.com/112503770/221423244-90d1e98b-a4c6-46bf-ad70-540dca22c25d.png)

Käyttöliittymän kautta voidaan lisätä tietoja helposti ja relaatiot toimivat, mutta luokkien sisällöt ilmenevät muodossa `Student object(1)`. Korjataksemme tämän voimme käydä muokkaamasssa models.py tiedostoa.

Models.py tiedostoon tehdyt relaatiot näkyvät webissä. Kuvassa lisätään Grade oliota, johon voidaan valita vain olemassa olevia student olioita.

![Relaatiotoimii](https://user-images.githubusercontent.com/112503770/221423253-8edf7c61-4193-4b23-8e60-d686607679b7.png)

Muokataan models tiedostoa, jotta nimet näkyy fiksusti.

    micro crm/models.py
    
![paivitetty luokat](https://user-images.githubusercontent.com/112503770/221423288-5f756c98-4936-4ecc-a594-32c4fd360f6f.png)

Tarkistetaan vielä weppisivulta:

![parempi nakuma](https://user-images.githubusercontent.com/112503770/221423302-98437166-17bc-498f-9269-c61c5512ebb7.png)

## Lähteet:

    https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/
    https://terokarvinen.com/2022/django-instant-crm-tutorial/
    https://virtualenv.pypa.io/en/latest/cli_interface.html
