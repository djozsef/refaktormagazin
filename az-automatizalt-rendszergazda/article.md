Kilencvenes évek. Valahol egy sötét szobában egy magányos alak ül egy CRT monitor előtt. Egyszer csak nyílik egy ajtó, világosság látszik, és félve lép be egy irodai alkalmazott, halkan megköszörüli a torkát, majd félhangon elkezdi a mondókáját: „...elveszett az egyik fájlom”. A magányos alak felnéz a monitorból, és a meg nem értett zsenik sóhajával hátra fordul...

<!--more-->

Ő a Rendszergazda. A drága pénzen vásárolt számítógépek nagyhatalmú ura. Ha mond valamit, a szava szent és sérthetetlen, aki felesel, azt rövid úton <a href="http://szabilinux.hu/moka/pokoli_operator.html">megmagyarázhatatlan műszaki hibák sorozata éri</a>, mintha megátkozták volna. Az oltára egyetlen hatalmas vasdobozban testesül meg: a szerver. Mindenki más számára egy ormótlan, hangos vasdoboz, ami indokolatlanul sokba kerül és indokolatlanul sok áramot fogyaszt. Ha valamilyen újabb programra lenne szükség, vagy netalán fogytán a nagy kegyelemmel kapott néhány megabájt hely, a Rendszergazdához kell fordulni. Majd hogy nem élet és halál ura, minden egyes programot, frissítést leellenőrzött és egyesével telepített fel. A tökéletes Rendszer.
<h3>Tíz évvel később...</h3>
Ugyanaz a szoba, ugyanaz a rendszergazda. A monitor egy másik, és az ormótlan vasdög helyét a korabeli formatervezésnek csúcsát képviselő, lilás színben tündöklő csinos doboz foglalja el. Továbbra is ormótlan, továbbra is hangos, és már nincs egyedül: egy egész szekrénnyi van ezekből a dögökből.

Az ajtó már nem lassan nyílik, hanem kávéval a kezében éppen hogy be nem rúgja a morcos kolléga. A tíz évvel ezelőtti alázatnak nyoma sincs, cseppet sem barátságos hangon vonja kérdőre a vén rókát, hogy miért fogyott már megint el a hely a szerverről.

A Rendszergazda nagy kelletlenül megnyitja az általa mélyen gyűlölt grafikus felületen a Novell menedzsment felületét és megkeresi a kelletlenkedő kolléga felhasználóját, majd néhány számot bepötyög. „Tessék, kész.”

A programok valóságos program-hegyekké nőtték ki magukat, a Rendszergazda már csak tessék-lássék nézte át őket, aztán néhányat a kifejezett rosszallása ellenére is csak-csak feltelepített.
<h3>Napjainkban</h3>
Hatalmas változások mentek végbe az elmúlt tíz évben. A Rendszergazda már nem ülhet a sötét szobában, a munkaügyi szabályoknak megfelelően legalább 500 lux fényerejű irodába kellett költöztetni, ezért kapott egy világos szobát. Persze nem egyedül, hiszen az iroda négyzetméter-ára borsósan drága, és a Rendszergazdát amúgy is túlfizetettnek érezte a vezetőség.

Egy csendes hétfő reggel, történetünk hőse a kávéját szürcsölve belép az irodába, a környezetéről nem sok tudomást véve. Már reggel amikor felkelt, megnézte, hogy csak két tucat hibajegy várja, így nem túlzottan aggódik a késése miatt. A szemén látszik, hogy az előző esti IRC-elés megint messze túl hosszúra sikerült. Nem sok tudomást vesz a környezetéről, így fel sem tűnik, hogy az iroda olyan, mint a felbolydult méhkas.

Hideg zuhanyként ébreszti fel félálmából, amikor az egyik fejlesztő odalép hozzá: „Öcsém, Te is jókor jössz be, hajnali 2 óta állunk.” Hideg fut végig a hátán... hogy a fenébe történhetett ez? Hiszen saját maga konfigurált mindent, a rendszer összes komponensét ő ellenőrizte le!

A Rendszergazda legrosszabb rémálma válik valóra. A vezetőség már jó ideje úgy érezte, hogy az üzemeltetés nem a megfelelő kerékvágásban halad, ezért felkért egy külsőst, hogy nézze át a rendszert. Az érkezése éppen egybe esik ezzel az ominózus nappal, így egy rossz nap még rosszabb lesz. Miközben kétségbeesetten próbálja megtalálni, hogy miért állt le az oldal, az egyik fejlesztő magyarázza az architektúrát a gyűlölt idegennek.

Két óra elteltével még mindig áll a rendszer, lassan ebéd idő lenne, ám erre gondolni sem lehet. Ott van a főnök a szobában, ujjaival idegesen dobol az asztalon. Megtörténik a lehetetlen: odahívja az idegent, hogy segítsen. Az odalép, majd néhány rövid kérdés után feldobja:
<blockquote>—„Nem lehet, hogy a switchben van a probléma?”
—„Az kizárt. Én programoztam fel.”
—„Na azért csak nézzük meg.”</blockquote>
Hősünk nagy morogva bejelentkezik a switchre, majd néhány rövid parancs után gyorsan be is zárná az ablakot, de az idegen megállítja, majd rövid nézelődés után megállapítja, hogy a switchből gyakorlatilag teljes egészében hiányzik a konfiguráció. A rendszergazda a homlokához kap: „Ó hogy az a! Beraktam a switch configot, de nem mentettem el és éjszaka volt egy rövid áramszünet!”
<h3>Az automatizálás</h3>
Ami ezután következik, nem kevésbé kellemes. Az idegen néhány hét alatt darabjaira szedi a rendszert, és egy tíz oldalas hibalistát ír, amiből a fele súlyos biztonsági vagy architekturális hiba: hiányzó biztonsági frissítések, az internetre kilógó kritikus szolgáltatások, hiányzó monitorozások díszes társasága sorakozik a papiron. A Rendszergazda majd' elsüllyed szégyenében, és egyszerűen nem érti: hogyan csúszhattak bele a tökéletes rendszerbe ilyen hibák?

A következő meetingen az idegen vázolja a tervet: automatizálni kell. Ennyi gépet, ennyi szolgáltatást nem lehet kézzel vezérelni. Nincs többet kézzel kókányolás, nincs több gyors tákolás, csak hogy menjen a rendszer valahogy, aztán úgy maradjon.

Puppet, Chef, Ansible, ezek a menők a versenyben. Választanak egyet. A Rendszergazdát nem érdekli, válasszanak. Ki hallott már olyat, hogy egy automatizmus konfiguráljon Linuxot? Hát még switchet? Meg hogy nem nézünk át minden szoftvert telepítés előtt? Jó, jó, az az özönvíz előtti nginx kicsit csúnya volt, de hát vettek volna fel több rendszergazdát. Ha nem két ember lenne két racknyi gépre, ez az egész nem lenne téma.

Megvan az új stratégia: a Rendszergazda a konfiguráció-menedzsment rendszerben megírja a szükséges modulokat, a programhoz pedig a fejlesztők mellékelnek egy rövidke konfigurációt, hogy hogyan fusson a szoftver az éles szerveren. Felügyelet nélkül. Észbontó.

További borzalmak következnek: a konfiguráció-menedzsment nem hogy a webszervert állítja be, hanem az adatbázisban a jogosultságokat is, és egy Jenkinst is megpiszkál, hogy a fejlesztő önállóan tudjon élesíteni. De hát a fejlesztőkben nem lehet bízni!

Végül betelik a pohár: a menedzsment kimondja az új kulcsszót: DevOps. A fejlesztő legyen kicsit rendszergazda, a rendszergazda legyen kicsit fejlesztő. Bullshit, gondolja a hősünk, és még aznap felmond.
<h3>Fél évvel később</h3>
Az idő állítólag minden emléket megszépít, legalábbis a Rendszergazda esetében ez így történt. Enged az egyik régi kolléga meghívásának, és elmennek sörözni.

Félig undorral, félig kiváncsian hallgatja a fejleményeket: az elején ugyan be-be borult a rendszer, amikor a fejlesztők mellényúltak, de szépen lassan megtanulták, hogy mit lehet és mit nem. Cserébe mindenhez van monitorozás automatikusan, nem kell foglalkozni a deploymenttel, sokkal kevesebb a napi nyűg is. Az új rendszergazda-csapat feje fölött sokkal kevesebbszer csapnak össze a hullámok, hosszabb távra terveznek.

A Rendszergazda megrázza a fejét, és a következő sör mellé a biztonság kedvéért rendel egy felest is. „Szép új világ...”
