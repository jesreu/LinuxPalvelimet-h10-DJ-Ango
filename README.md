# LinuxPalvelimet-h10-DJ-Ango
    Kirjoittanut: Jesse Reunamo
    Kurssi:       Linux-palvelimet
    Linkki:       https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/

## a)
Luodaan oma tietokantasovellus käyttämällä django kehysympäristöä.

### Kehitysympäristön luominen
Aloitetaan prosessi asentamalla virtualenv paketti, jolla voidaan luoda virtuaalisia pyhton ympäristöjä. Kannattaa myös ajaa komento `man virtualenv` asennuksen jälkeen, jotta voit tutustua työkaluun.

    sudo apt-get -y install virtualenv
    man virtualenv

kuve man komennosta


Nyt voimme käyttää asennettua virtualenv ohjelmaa. Voimme ajaa alapuolella olevan komennon, jossa luomme uuden virtuaaliympäristön käyttöömme. Komennon liput: --system-site-packages: mahdollistaa virtuaaliympäristön käyttää ympäristön ulkopuolisia paketteja.  -p lippu määrittää käytetyn python version ja lopussa env/ on sijaintina. 

    virtualenv --system-site-packages -p python3 env/

kuvet lipuista

Otetaan virtuaaliympäristö käyttöön komennolla:

    source env/bin/activate
Tarkistaa, että asennetaan oikeaan paikkaan komennolla:

    which pip

    micro requirements.txt
    
    pip install -r requirements.txt
    django-admin --version
    
### Djangon käynnistäminen  

    django-admin startproject sivuco
    cd sivuco
    ./manage.py runserver
    
    ./manage.py makemigrations
    ./manage.py migrate
    
 ### Admin käyttäjän luominen 
Lopeta severin ajaminen painamalla `ctrl + c`, jotta voimme ajaa komentoja samalla ikkunalla.

Salasanan luomiseen:

    sudo apt-get install pwgen
    pwgen -s 20 1
    
Adminkäyttäjän luominen aja alapuolella oleva komento ja vastaa sen haluamiin kysymyksiin.

    ./manage.py createsuperuser
    ./manage.py runserver
    
Testaan onnistuiku käyttäjän lisääminen menemällä `127.0.0.1:8000/admin/` osoitteeseen ja kirjautumalla sinne.

kuve

### Toisen käyttäjän luominen

Luodaan toinen käyttäjä webbiliittymän kautta, koska oikealle käyttäjälle ei tulisi antaa admin käyttäjää. Voit lisätä uuden käyttäjän klikkaamalla `+ Add` vaitoehtoa Users kentän oikealla puolella

kuve

Sivu kysyy käyttäjän nimen, salasanan ja muut tiedot. Täytä ne hyvän tietoturvan mukaisesti. Kun olet tehnyt uuden käyttäjän, voit muokata käyttäjän oikeuksia klikkaamalla `Users` kenttää, joka avaa sivun missä näet kaikki käyttäjät.

kuve

Klikkaamalla lisäämäsi käyttäjää, (minun tapauksessa EssiEsimerkki) aukeaa sivu, jossa voit asettaa käyttäjälle tarvittavat oikeudet. 

kuve

Nyt voit kirjautua ulos admin käyttäjältä ja vaihtaa normaalille käyttäjälle.

### Tietokannan luominen b)
Luodaan kansio crm (customer relational management) applikaatiolle

    ./manage.py startapp crm
    
    micro sivuco/settings.py
    
kuve

    micro crm/models.py

kuve


Ajetaan komennot:

    ./manage.py makemigrations
    ./manage.py migrate
Ajatessa ilmeni virhe:

kuve:

Oletan, että kyseessä on kirjoitusvirhe, joten ajan kommennon `micro crm/models.py` ja korjaan kuvassa näkyvän ison L kirjaimen. Ajan uudelleen komennot:
    
    ./manage.py makemigrations
    ./manage.py migrate

Rekisteröidään admin sivulle tehdyt modelit, jotta ne näkyvät weppisivulla.

    micro crm/admin.py
    
kuve

Käynnistetään serveri vielä, jotta voidaan tarkistaa tulivatko luokat näkyviin.
    
    ./manage.py runserver
    
kuve

Käyttöliittymän kautta voidaan lisätä tietoja helposti ja relaatiot toimivat, mutta luokkien sisällöt ilmenevät muodossa `Student object(1)`. Korjataksemme tämän voimme käydä muokkaamasssa models.py tiedostoa.

Relaatiot näkyvät webissä:

kuve

Muokataan models tiedostoa:

    micro crm/models.py
    
kuve

Tarkistetaan vielä weppisivulta:

kuve

## Lähteet:

    https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/
    https://terokarvinen.com/2022/django-instant-crm-tutorial/
    https://virtualenv.pypa.io/en/latest/cli_interface.html
