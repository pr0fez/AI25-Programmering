## Terminalens historia
Här är några riktiga terminaler i ordning från äldst till nyast:

<img src="https://upload.wikimedia.org/wikipedia/commons/7/76/ASR-33_1.jpg" alt="ASR33" width="200"/>
<img src="https://sharktastica.co.uk/resources/images/typewriters/onierstrasz_2741.jpg" alt="IBM2741" width="200"/>
<img src="https://upload.wikimedia.org/wikipedia/commons/9/9f/DEC_VT100_terminal_transparent.png" alt="VT100" width="200"/>
<img src="https://upload.wikimedia.org/wikipedia/commons/8/81/Datapoint-2200.jpg" alt="Datapoint-2200.jpg" width="200">

Just dessa har alla särskild historisk betydelse -- sist är en maskin som kan sägas vara den första massproducerade (person-)datorn som vi känner den idag, en så kallad "intelligent terminal", Datapoint 2200. Den har inte någon mikroprocessor, utan en s.k. TTL processor. 

Ingen använder sådana längre, men textbaserade interface har ett arv från början av informationsåldern. I dag emulerar / virtualiserar vi terminalerna.

En terminal kallas även en `tty` efter TeleType, som var de första terminalerna. De hade som synes ovan inte skärmar utan skrivare. Här är de i användning under 2:a världskriget:

![TeleType](https://upload.wikimedia.org/wikipedia/commons/8/89/WACsOperateTeletype.jpg)

En intressant sidnot är att allt som rörde datorer innan 1970-talet var kvinnodominerat. Det är först med den (amerikanska) stereotypen av en datanörd i sina föräldrars källare med en PC som området blir mansdominerat. Datorer associerades med just teletype och skrivmaskiner -- vilket ansågs vara kvinnliga verktyg använda av sekreterare och växeltelefonister. 

Dessa interface lever kvar i POSIX. Inloggningsskärmen på Linux är oftast `tty1` och `tty2`, men på äldre system är `tty6` ofta den grafiska inloggningen. På linux kan du trycka `Ctrl+Alt+(F1-F7)` för att byta `tty`. Varje `tty` stödjer en (separat) inloggning. POSIX system är i grunden nätverksbaserade och fleranvändarsystem. Som Solaris® slogan uttryckte det: "The Network is the Computer".


## Filer och Kataloger
Öppna en terminalemulator. I Windows kan du använda PowerShell, git-bash eller en WSL terminal. På POSIX system finns många alternativ; Mac OS X har en anrik terminal emulator som har sina rötter i den banbrytande NeXTSTEP grafiska miljön. Tekniskt sett är terminalen och skalet inte samma sak -- terminalen huserar ett text-baserat skal, men begreppen används ganska utbytligt. 

Med en terminal (emulator) öppen, använd följande kommandon:

`pwd`
Print Working Directory

`ls`
List Directory.

`man mkdir`

`mkdir --help`

Undersök vad flaggan `-p` gör. 

`mkdir -p min_katalog/tom_katalog`
Make Directory

`cd min_katalog`
Change Directory

`rmdir tom_katalog`
Remove Directory -- endast tomma kataloger!

`echo "Hello World" > min_fil.txt`
Dirigera om text från eko-kommandot till en fil. 

`mv min_fil.txt min_fil`
Move -- byta namn är en sorts flytt. Filändelser är inte obligatoriskt.

`cp min_fil min_fil.txt`
Copy. Filändelser är ofta bra att ha. Körbara program brukar dock inte ha någon filändelse i POSIX system.

`rm -r min_katalog`

`rm min_fil`

Remove

`cd ..`
Byt katalog till en nivå ovanför. Kolla vilken katalog du är i.

`rm min_katalog/*`
Det finns egentligen aldrig anledning att använda `*` ensamt tillsammans med rm. Detta är en mycket säkrare form.

`touch min_katalog/.read_only.secret`
Uppdaterar tidsstämpeln på en fil -- skapar filen om den inte finns. Filer som börjar med `.` listas inte av `ls` utan flaggan `-a`. 

`chmod a-w min_katalog/.read_only.secret`
Change Mode. Ovan rad tar bort skrivrättigheter för alla användare.

`rm -r min_katalog`
Remove recursive. Tar obort min_katalog och allt som ligger i den, men frågar om skrivskyddade filer skall tas bort.
`rm -rf min_katalog`
Ställer inga frågor, utan tar bort allt ovillkorligen.


`find / -iname "*.cfg" 2> /dev/null`
Letar igenom hela datorn efter filer med ändelsen `.cfg` och omdirigerar `stderr` till intet (`/dev/null` är ett tomt interface -- allt som hamnar där försvinner). Alltså skrivs inga felmeddelanden ut.

`find / -iname "*.cfg" 2> /dev/null > result.txt`
Samma som ovan, men resultatet skrivs till fil.

`head -n 12 resultat.txt`
Visar första tolv raderna i filen.

`tail -n 12 resultat.txt`
Visar tolv sista raderna i filen.

`less resultat.txt`
Interaktiv textläsare. Hjälpmeny `h`. Avsluta med `q`. 

`grep -v etc resultat.txt | less`
Söker igenom resultatet efter rader som _inte_ innehåller `etc` och vidarebefodrar `stdout` till `stdin` för kommandot `less`.

## Systemkommandon
`uname -a`
Visar versionsinformation från systemet, tex vilken Linux variant det är. Inte hårt standardiserat, så kan se väldigt olika ut på olika system.

`df -h`
Visar diskanvändning.

`du -sh $HOME/*`
Visar storleken på varje fil och katalog i hemkatalogen.

`top`
Visar interaktivt körande processer och prestandainformation. Tryck `h` för hjälp. Avsluta med `q`.

`ps aux` BSD syntax

`ps -ef` POSIX syntax

Listar utförligt alla körande processer för alla användare.

`ps | grep python` listar användarens körande pythonprogram.

`kill 3852` 
Avsluta en körande process. Process ID hittas med `ps`.

`kill -9 8364`
Om ett program vägrar avsluta kan man skicka med flaggan `-9`. Då skickas en `SIGKILL` signal istället för den mer snälla `SIGINT`. Programmet får ingen chans alls att spara något eller stängas av snyggt, det dör mitt i vad det än håller på med.

## Nätverk

`ifconfig` äldre system

`ip address show` nyare system

Visar nätverksinformation och tilldelad IP address.

`ping google.com`
Kollar om google.com är nåbar från datorn.

`curl http://example.com`
Hämtar innehåll från URLer. Kan användas till mycket avancerade interaktioner.

`wget http://example.com/file.zip`
Hämtar filer från URLer. 

`ssh user@hostname`
Secure Shell. Loggar in som `user` på maskinen `hostname` med en SSL krypterat session. Det faktiska skalet kommer från maskinen i andra ändan.

`scp file.txt user@hostname:/path/to/destination`
Kopierar filer över en SSL krypterad länk.

## Övrigt
`alias ll='ls -l'`
Skapar ett kortkommando för `ls -l`. Efter raden ovanför kan man alltså skriva `ll` i terminalen och få samma svar som `ls -l`. Finns motsvarande i git.

`source ~/.bashrc` eller `. ~/.bashrc`
Kör ett shell-skript i nuvarande skal.

`export PATH=$PATH:/new/path`
Sätter miljövariabeln PATH till det gamla värdet plus `:/new/path`. 

`tar -czvf archive.tar.gz /path/to/directory`
Tape ARchive. Inget band inblandat längre, men detta skapar ett komprimerat bibliotek med namnet `archive.tar.gz` av alla filer och kataloger i `/path/to/directory`. När den är komprimerad kallas detta en "tar-ball". 
