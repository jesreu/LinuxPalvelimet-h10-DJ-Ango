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
    
    django-admin startproject sivuco
    
## Lähteet:

    https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/
    https://terokarvinen.com/2022/django-instant-crm-tutorial/
    https://virtualenv.pypa.io/en/latest/cli_interface.html
