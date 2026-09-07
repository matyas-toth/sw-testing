# 1. Hibakeresés DiscountCalculator-ban

- A szöveg azt írja, hogy "10.000 forint alatt nincs kedvezmény", de a kód 10.000 forintnál se ad kedvezményt.
- Csak akkor ad 5% kedvezményt, ha 10.001 forint minimum, miközben 10.000 forint a határ amit a szöveg említ.
- A szöveg 10% kedvezményt említ 25.000 - 49.999 között, de a kód 10%-ot ad ha <= 50.000, azaz 50.000 forintnál is 10%-ot kapsz.
- A 15%-os kedvezményt csak 50.001 forinttól kapja meg a felhasználó, a szöveg 50.000-et említ.
- az "isVip" if-clauseban nem +0.05-el adunk hozzá 5% kedvezményt, hanem +5-tel, effektíven 500% kedvezményt adva
- a kedvezményt kifejező számot csak kivonjuk a végösszegből, a helyes az orderValue - (orderValue*discount) lenne

# 2. Hibakeresés ParkingFeeCalculatorban

- A specifikáció szerint az első 15 perc ingyenes, viszont minutes < 15-tel ellenőriz a kód, így aki 15 percig parkol az már fizet.
- Megkezdett órát lefele kerekít, floor helyett ceil szükséges
- A vip kedvezmény nem jó, 20 forintot von le, nem 20%-ot
- A negatív parkolási idő nincs kezelve

# 3. Hibakeresés CinemaTicketCalculatorban
- A specifikáció szerint 6 éves kor alatt ingyenes a jegy, de a kód age <= 6-ot ellenőriz, így a 6 éves is ingyen kapja, pedig neki már a 30%-os kedvezmény járna.
- A specifikáció szerint 65 éves kortól 40% kedvezmény jár, de a kód age > 65-öt ellenőriz, így a pontosan 65 éves nem kapja meg a kedvezményt.
- A specifikáció szerint egyszerre csak a legnagyobb kedvezmény alkalmazható, de a kód a kor alapján járó kedvezmény után a diákkedvezményt is ráteszi.
- Például egy 17 éves diák először 30% kedvezményt kap, majd arra még további 20%-ot, miközben csak a nagyobb, 30%-os kedvezményt szabadna alkalmazni.
- A 3D felár fixen 800 forint, a kód viszont price * 1.8-at számol, azaz 80%-kal növeli az aktuális jegyárat.
- A 3D felárra nem vonatkozik kedvezmény, ezért azt a kedvezmény kiszámítása után fixen +800 forintként kellene hozzáadni.
- A jelenlegi kódban egy 6 év alatti néző 3D film esetén is 0 forintot fizet, mert 0 * 1.8 továbbra is 0, pedig a 800 forintos 3D felárat ki kellene fizetnie.
- A negatív életkor nincs kezelve.
- A 120 év feletti életkor nincs kezelve.

# 4. Hibakeresés ExamGradeCalculatorban
- A vizsga akkor is sikertelen, ha csak az egyik minimumfeltétel nem teljesül, a kód viszont theory < 30 && practice < 20 feltételt használ, így csak akkor ad automatikusan - 1-est, ha mindkettő egyszerre elégtelen.
- Az && helyett || szükséges, mert már az is bukást jelent, ha elméletből nincs meg a 30 pont vagy gyakorlatból nincs meg a 20 pont.
- A 2-es jegy 50-59 pont között jár, de a kód total <= 60-at használ, így 60 pontra is 2-est ad.
- A 3-as jegy 60-69 pont között jár, de a kód total <= 70-et használ, így 70 pontra is 3-ast ad.
- A 4-es jegy 70-84 pont között jár, de a kód total <= 85-öt használ, így 85 pontra is 4-est ad.
- 60 ponttól már 3-as, 70 ponttól már 4-es, 85 ponttól pedig már 5-ös jegyet kellene adni.
- Nincs ellenőrizve, ha az elméleti pontszám negatív.
- Nincs ellenőrizve, ha az elméleti pontszám nagyobb 60-nál.
- Nincs ellenőrizve, ha a gyakorlati pontszám negatív.
- Nincs ellenőrizve, ha a gyakorlati pontszám nagyobb 40-nél.
- A specifikáció szerint érvénytelen pontszám esetén hibát kell jelezni, de a kód ilyen esetekben is megpróbál jegyet számolni.