# Hur man skapar dual boot med Kubuntu och Windows 

## Innan du börjar  
- Strömkabel ikopplad till datorn
- Linux kubuntu USB insatt i datorn

## Installation
### Stäng av Secure Boot
- Stäng av datorn helt
- Sätt på datorn och tryck upprepat på F10
- Navigera till 'Security' > 'Secure Boot Configuration'
- Stäng av Secure Boot
- Gå tillbaka till 'Main'

### Boota installationsmediat
- Sätt i USB-stickan
- Välj 'Save Changes and Exit', sedan 'Yes'
- Tryck upprepat på F9
- Välj 'UEFI - Kingston DataTraveler [...]'
- Välj 'Try or Install Kubuntu'

## Vad du väljer under installationen
- För nätverksanslutning, välj 'WiFi tcstenungsund' och skriv i lösenordet
- Klicka 'Install Kubuntu'
- Välj Europe, Stockholm som tidszon
- För tangentbordslayout, välj 'Swedish' och 'Default'
- Välj 'Normal Installation'
- Välj 'Install alongside' och tryck på 'nvme0n1p3', välj att använda ungefär hälften av partitionen
- Fyll i uppgiterna i användarformuläret
- Verifiera att samtlig information är överensstämmer med tidigare instruktioner och välj därefter 'Install'

## Det första du bör göra när du är klar med installtionen  
