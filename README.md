# Hur man skapar dual boot med Kubuntu och Windows 

## Innan du börjar  


## Boota om och sätt igång installationen  


## Vad du väljer under installationen  


## Det första du bör göra när du är klar med installtionen 

Det är fyra saker som du ska göra efter att du har installerat Kubuntu, och det är:  
- Ändra skalan på skärmen (frivilligt)  
- Ladda ner Firefox Developer Edition  
- Ladda ner VSCodium  
- Ladda ner Git  

---

### 1. Ändra skalan på skärmen (frivilligt)  
Det första du bör göra efter att du är klar med installationen är att kolla så att skalan på skärmen är rätt.  

1. Tryck på **Windows-knappen** och sök efter *System Settings*.  
2. Gå in på *Settings* under *Input & Output* och navigera till *Display & Monitor*.  
3. Under *Display & Monitor*, kontrollera att skalan (*Scale*) är satt på **100%**.  

---

### 2. Installera Firefox Developer Edition  

**FÖRST**. Skapa en katalog för att lagra APT-arkivets nycklar:  
```
sudo install -d -m 0755 /etc/apt/keyrings
```

**FÖR DET ANDRA**. Importera Mozilla APT-arkivets signeringsnyckel:

```
wget -q https://packages.mozilla.org/apt/repo-signing-key.gpg -O- | sudo tee /etc/apt/keyrings/packages.mozilla.org.asc > /dev/null
```

**TREDJE**. Fingeravtrycket ska vara (35BAA0B33E9EB396F59CA838C0BA5CE6DC6315A3). Du kan kontrollera det med följande kommando:

```
gpg -n -q --import --import-options import-show /etc/apt/keyrings/packages.mozilla.org.asc | awk '/pub/{getline; gsub(/^ +| +$/,""); if($0 == "35BAA0B33E9EB396F59CA838C0BA5CE6DC6315A3") print "\nThe key fingerprint matches ("$0").\n"; else print "\nVerification failed: the fingerprint ("$0") does not match the expected one.\n"}'
```

**FJÄRDE**. lägg till Mozilla APT-arkivet i din källlista:

```
echo "deb [signed-by=/etc/apt/keyrings/packages.mozilla.org.asc] https://packages.mozilla.org/apt mozilla main" | sudo tee -a /etc/apt/sources.list.d/mozilla.list > /dev/null
```

**FEMTE**. Konfigurera APT för att prioritera paket från Mozilla-arkivet:

```
echo '
Package: *
Pin: origin packages.mozilla.org
Pin-Priority: 1000
' | sudo tee /etc/apt/preferences.d/mozilla
```

**SJÄTTE**. Uppdatera din paketlista och installera Firefox .deb-paketet:

```
sudo apt-get update && sudo apt-get install firefox-devedition
```

Nu är **Firefox-Developer-Edition** installerat.

---
**För att installera VSCodium:** Öppna en terminal i Kubuntu och använd följande kommando för att hämta utvecklarens GPG-signaturnyckel och lägga till den i ditt system. På så sätt kommer ditt Kubuntu-system att lita på de paket som är signerade av denna utvecklare.
```
sudo wget https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/master/pub.gpg -O /usr/share/keyrings/vscodium-archive-keyring.asc
```

Nästa steg är att lägga till arkivet i systemets sources.list-fil. På så sätt vet ditt Kubuntu-system varifrån det ska hämta paketet.
```
echo 'deb [ signed-by=/usr/share/keyrings/vscodium-archive-keyring.asc ] https://paulcarroty.gitlab.io/vscodium-deb-rpm-repo/debs vscodium main' | sudo tee /etc/apt/sources.list.d/vscodium.list
```

Uppdatera den lokala paketcachen så att ditt system är medvetet om paketen från det nyligen tillagda arkivet.
```
sudo apt update
```

Nu är du redo att installera VSCodium på Kubuntu:
```
sudo apt install codium
```

---
Git ska vara intallertat från början men om det inte är det så laddar du ner Git med detta kommandot:
```
sudo apt-get install git
```
