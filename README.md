# Hur man skapar dual boot med Kubuntu och Windows 

## Innan du börjar  


## Boota om och sätt igång installationen  


## Vad du väljer under installationen  


## Det första du bör göra när du är klar med installtionen 

Det är fyra sakaer som du ska göra after att du har installerat Kubuntu och det är:
Ändra skalan på skärmen(Frivillig)
Ladda ner FireFox-Develepor-Edition.
Ladda ner VsCodium
ladda ner Git
----------
Första du bör göra efter att du är klar med installationen, är att kolla så att skalan på skärmen är rätt. 
Trycka på windows knapen och sök på system settings. Gå in på settings under Input & Output och navigera till Display & Monitor. 
Under Display & Monitor kolla så att skalan (Scale) är satt på 100%.

------------ 
Det andra du ska göra är att installera FireFox-Develepor-Edition.
FÖRST. Skapar vi en katalog för att lagra APT-arkivets nycklar:

```
sudo install -d -m 0755 /etc/apt/keyrings
```

FÖR DET ANDRA. Importera vi Mozilla APT-arkivets signeringsnyckel:

```
wget -q https://packages.mozilla.org/apt/repo-signing-key.gpg -O- | sudo tee /etc/apt/keyrings/packages.mozilla.org.asc > /dev/null
```

TREDJE. Fingeravtrycket ska vara (35BAA0B33E9EB396F59CA838C0BA5CE6DC6315A3). Du kan kontrollera det med följande kommando:

```
gpg -n -q --import --import-options import-show /etc/apt/keyrings/packages.mozilla.org.asc | awk '/pub/{getline; gsub(/^ +| +$/,""); if($0 == "35BAA0B33E9EB396F59CA838C0BA5CE6DC6315A3") print "\nThe key fingerprint matches ("$0").\n"; else print "\nVerification failed: the fingerprint ("$0") does not match the expected one.\n"}'
```

FJÄRDE. lägg till Mozilla APT-arkivet i din källlista:

```
echo "deb [signed-by=/etc/apt/keyrings/packages.mozilla.org.asc] https://packages.mozilla.org/apt mozilla main" | sudo tee -a /etc/apt/sources.list.d/mozilla.list > /dev/null
```

FEMTE. Konfigurera APT för att prioritera paket från Mozilla-arkivet:

```
echo '
Package: *
Pin: origin packages.mozilla.org
Pin-Priority: 1000
' | sudo tee /etc/apt/preferences.d/mozilla
```

SJÄTTE. Uppdatera din paketlista och installera Firefox .deb-paketet:

```
sudo apt-get update && sudo apt-get install firefox-devedition
```

Nu är FireFox-Develepor-Edition installerat.

-----------
Git ska vara intallertat från början men om det inte är det så laddar du ner Git med detta kommandot:
```
sudo apt-get install git
```
