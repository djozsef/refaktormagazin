Talán nincs még egy olyan téma a fejlesztés terén, ahol annyi hibát és téves értelmezést látok, mint az időkezelésben. Tény, hogy valóban nem egyszerű kérdés, rengeteg mindennel kell foglalkoznunk, az időzónáktól kezdve, a téli/nyári időszámításon át, a szökőmásodpercekig.

Sokan azt gondolják, hogy elegendő minden időt UTC-ben tárolni, ám sajnos ez még mindig nem elegendő ahhoz, hogy helyesen kezeljük az idő-jellegű adatainkat.

<!--more-->

## Az elmélet

A számítástechnika hajlnalán az időszámításra egy igen egyszerű megoldást választottak: 1970\. január 1-étől számolták a másodperceket, UTC időzónában. Ez az időszámítás lett a [UNIX timestamp](https://hu.wikipedia.org/wiki/Unix-id%C5%91). A UNIX idő hatalmas előnye, hogy egyszerű vele számolni. Az idő-adatok egész szám formában tárolhatóak, és két idő közötti különbség egy egyszerű matematikai művelettel kiszámolható. Egy óra 3600 másodperc, egy nap 86400 másodperc.

A rendszer megalkotói azonban nem számoltak azzal, hogy ezt a fajta megbízhatóságát a fejlesztők mennyire felülbecsülik. Az UTC időzónát ugyanis nem szabályos időközönként hozzáigazítják az UT1 időzónához, ami közvetlenül követi a Föld forgását. Ezt a hozzáigazítást egy úgynevezett szökőmásodperc betoldásával oldják meg. Tehát lesz olyan nap, amely nem 86400, hanem 86401 másodpercből áll. Egy ilyen szökőmásodperc volt 2015\. június 30 23:59:60, azaz a nap utolsó másodperce nem 59 volt, hanem 60\. Ez a látszólag ártalmatlan plusz másodperc hatalmas problémákat tud okozni, mint azt az elmúlt pár szökőmásodperc bizonyította is.

Tovább bonyolítja a helyzetet, ha nem UTC-ben szeretnénk kezelni az időt, hanem helyi időben. Ekkor ugyanis helytől függően évente kétszer bejön az óraátállítás is.

## Példa

Nézzünk egy példát, a jelenlegi időhöz hozzáadunk 3 napot:

[fusion_tabs design="classic" layout="horizontal"]
[fusion_tab title="PHP"]<pre><code class="php">echo(
  date(
    "Y-m-d H:i:s",
    time()+86400*3
  )
);</code></pre>[/fusion_tab]
[fusion_tab title="Python" icon=""]<pre><code class="python">import time
import datetime
timestamp = int(time.time()) + 86400*3
print(datetime.datetime.fromtimestamp(timestamp).strftime('%Y-%m-%d %H:%M:%S'))</code></pre>[/fusion_tab]
[/fusion_tabs]

Ez szép és jó, jó eséllyel pontosan megadja a jelenlegi időt 3 nap múlva. De nézzük, mi történik, ha 2012\. március 23 14:00-t vesszük, CEST időzónában:

[fusion_tabs design="classic" layout="horizontal"]
[fusion_tab title="PHP"]<pre><code class="php">date_default_timezone_set('Europe/Budapest');
echo(
  date(
    "Y-m-d H:i:s",
    mktime(23, 0, 0, 3, 23, 2012)+86400*3
  )
);</code></pre>[/fusion_tab]
[fusion_tab title="Python" icon=""]<pre><code class="python">import datetime import time import pytz

d = datetime.datetime(2012, 3, 23, 23, 0, 0, 0, pytz.timezone('Europe/Budapest'))
unixtime = time.mktime(d.timetuple())

print(
  datetime.datetime.fromtimestamp(
    unixtime + 86400 * 3,
    pytz.timezone('Europe/Budapest')
  ).strftime('%Y-%m-%d %H:%M:%S')
)</code></pre>[/fusion_tab]
[/fusion_tabs]

Azt várnánk, hogy március 26\. 23:00-t kapunk, helyette azonban március 27-én 00:00-t kapunk. Ha egyszerűen levágjuk az óra részt, vagy kerekítünk, akkor nem azt a napot kapjuk, amit várunk. Ez például egy szolgáltatás lejáratnál adott esetben katasztrofális következményekkel járhat.

## Változások az időzónákban

Időnként előfordul, hogy egy-egy ország politikai vagy gazdasági okokból úgy dönt, hogy időzónát vált vagy téli/nyári időszámítást vezet be. Ilyen történt például 2011-ben, amikoris Samoa egy egész napot kihagyva átugrott a dátumválasztó vonal egyik oldaláról a másikra.

Időnként sajnos szükség van arra, hogy visszamenőlegesen is tudjunk időt számolni, így ez igen csak bonyolulttá tenné a programlogikánkat, ha kézzel szeretnénk implementálni.

## Időkezelés modern számítógépes rendszerekben

Mint látjuk, az időkezelés pusztán másodperc alapon minimum problémás. Szerencsére az IANA, a nemzetközi számkiosztásért felelős szervezet, egy [naprakész adatfájlt tart fent](https://www.iana.org/time-zones) az ilyen változásokról. Ezeket gyakran _tz_, _tzdata_ vagy _zoneinfo_ néven is emlegetjük.

Szerencsére a zoneinfo adatbázis kezelését nem nekünk kell leprogramoznunk, ezt az operációs rendszerhez mellékelt programkönyvtárak megoldják. A modern programnyelvek ezeket a könyvtárakat felhasználva függvényeket vagy osztályokat biztosítanak a megfelelő időkezeléshez.

Az előző példát véve, nézzük hogyan kellene ezt helyesen megoldani:

[fusion_tabs design="classic" layout="horizontal"]
[fusion_tab title="PHP"]<pre><code class="php">date_default_timezone_set('Europe/Budapest');
$date = new DateTime('2012-03-23 23:00:00');
$date->add(new DateInterval('P3D'));
echo $date->format('Y-m-d H:i:s');</code></pre>[/fusion_tab]
[fusion_tab title="Python" icon=""]<pre><code class="python"></code></pre>[/fusion_tab]
[/fusion_tabs]

Ha ezt a kódot lefuttatjuk, a várt eredményt kapjuk: 2013-03-26 23:00:00.

## Összegzés

A mai napig nincs tiszta fogalmunk az idő múlásáról, és a bolygónk forgásához próbáljuk igazítani, ami egy tökéletlen módszer. Sajnos az alternatív időszámolási rendszerek nem terjedtek el széles körben, ezért a jelenlegi rendszerrel kell dolgoznunk.

Tekintettel a feladat komplexitására, senkinek nem javaslom, hogy saját maga próbálja meg implementálni az időkezelést, inkább használja a nyelvben közvetlenül, vagy függvénykönyvtárak által biztosított API-kat.
<div class="tip">Néha tényleg szükség van arra, hogy tényleg másodperceket számoljunk. Ilyenkor nagyon óvatosan kell eljárni, hogy a futtatókörnyezet időzóna-beállításai, és a szökőmásodpercek ne befolyásolhassák az eredményt.</div>
