# 1. Hibakeresés DiscountCalculator-ban

- A szöveg azt írja, hogy "10.000 forint alatt nincs kedvezmény", de a kód 10.000 forintnál se ad kedvezményt.
- Csak akkor ad 5% kedvezményt, ha 10.001 forint minimum, miközben 10.000 forint a határ amit a szöveg említ.
- A szöveg 10% kedvezményt említ 25.000 - 49.999 között, de a kód 10%-ot ad ha <= 50.000, azaz 50.000 forintnál is 10%-ot kapsz.
- A 15%-os kedvezményt csak 50.001 forinttól kapja meg a felhasználó, a szöveg 50.000-et említ.
- az "isVip" if-clauseban nem +0.05-el adunk hozzá 5% kedvezményt, hanem +5-tel, effektíven 500% kedvezményt adva
- a kedvezményt kifejező számot csak kivonjuk a végösszegből, a helyes az orderValue - (orderValue*discount) lenne

# 2. Hibakeresés ParkingFeeCalculatorban

