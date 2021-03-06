# LF-Tools

LT-Tools är en *extension* till Visual Studio Code med en uppsättning funktioner för att underlätta utveckling av Progress program i Länsförsäkringars miljö. Utvecklingsmiljön har bland annat *IntelliSence*, *Code Outline*, *Syntax highligting*, *Syntax checking* och viss integration med TFS.

## Installation

Ladda ner och installera Visual Studio Code. Installera därefter extension LF-Tools. Alla nedanstående funktioner blir då tillgängliga.

### Arbetskatalog (Workspace folder)

Vilken folder som helst kan göras till en LF-Tools-folder genom att kopiera in följande kataloger och filer i rooten på arbetskatalogen:

```abl
.lftools
    .lftools.config.json
    db.dict.winsure.json
.vscode
    launch.json
    settings.json
```

En grunduppsättning av dessa filer hittar du under **X:\01 System\Combi\LFTools** för Combi och under **X:\01 System\Ture\LFTools** för Ture.
Grundinställningarna pekar ut Combi Förvaltning PT1 för Combi och Ture Förvaltning PT1 för Ture som förvald kompilerings och kör-miljö.

## Features

Nedan följer en beskrivning av utvecklingsmiljöns funktioner.

### Editorn

Utvecklingsmiljön är baserad på Microsoft Visual Studio Code som i sig själv är en kodeditor i världsklass. Den innehåller en hel del riktigt bra funktioner för att skriva kod. Med LF-Tools som tillägg är den ett utmärkt verktyg för att hantera Progresskod i Länsförsäkringars miljö.  Här följer några godbitar av vad *VS Code* i sig har inbyggt.

#### Workspace

Tydlig och översiktlig arbetsyta som man enkelt kan ändra tema på så att det passar en själv.
**Mörkt tema**
![Image of Workspace with dark theme](images/vscode-workplace-dark.png)

**Ljust tema**
![Image of Workspace with light theme](images/vscode-workplace-light.png)

Till vänster på arbetsytan visas öppna filer och en lista med alla filer som finns i arbets-foldern. Nere till vänster visas en outline av alla procedurer och funktioner i den nu öppna filen.

Alla öppna filer visas som tabbar över själva arbetsytan. I bilderna ovan ser vi att *forsbesk.p* är öppet och aktivt för redigering och att XMLSkapare.cls är öppen men inte aktiverad.

Till höger på arbetsytan visas en förminskad bild av hela filens innehåll så att man lätt kan se var i filen man just nu redigerar.

#### Bra redigeringkommandon att komma ihåg

* `Alt`+`Pil Upp` och `Alt`+`Pil Ner` flyttar raden man står på uppåt eller nedåt
* `Shift`+`Alt`+`Pil Upp` och `Shift`+`Alt`+`Pil Ner` skapar en kopia av raden man står på ovanför eller under
* `Ctrl`+`Shift`+`K` tar bort raden man har sin cursor på
* `Ctrl`+`K` `Ctrl`+`C` Kommentarsmarkerar raden man står på eller alla markerade rader om flera är markerade
* `Ctrl`+`K` `Ctrl`+`U` Tar bort kommentarsmarkering på raden man står på eller alla rader om flera är markerade
* `Ctrl`+`J` Togglar panelen för *Problems*, *Output*, *Debug consol* och *Terminal*

##### *Multi cursor*-funktioner

* `Ctrl`+`Shift`+`L` markerar alla förekomster av ordet man har sin cursor över eller har markerat
* `Ctrl`+`D` markerar ordet man har sin cursor över. Om ordet redan är markerat så markeras nästa förekomst av ordet

När flera ord är markerade samtidigt och skriver något så ändras alla markerade ord samtidigt. Nedan bild visar när jag trycker `Ctrl`+`D` ett antal gånger och sedan skriver.

![Multi cursor image](images/multicursor.gif)

För att läsa mer om alla kommandon i VS Code, gör så här...

![Keyboard Shortcuts](images/keyboard-shortcuts.gif)

VS Code har inte alla kommandon i menyn utan man når dem genom att trycka `Ctrl`+`Shift`+`P`. En lista med alla kommandon visas och genom att skriva det man är ute efter filtreras de kommandon man är ute efter fram i listan.

### *IntelliSence*

IntelliSence hjälper till och ger förslag på vad du ska skriver i koden. Exempelvis kan du börja skriva ett tabellnamn så som `T01`. Då visas en lista med alla tabeller som börjar på T01. Samma gäller även för variabler, procedurer och funktioner, börjar man skriva ett namn så visas en lista med möjliga alternativ. Det här gör att det blir färre stavfel och kodskrivandet går klart snabbare.

Om du är osäker på vad en varaiabel har för datatyp är det bara att ställa muspekaren över variablen så visas datatypen och var den är deklarerad.

Om du behöver veta vad en procedur eller funktion gör, ställ markören på procedur- eller funktions-namnet och klicka `F12` så hoppar du direkt till definitionen av proceduren eller funktionen. Tryck `Alt`+`Pil vänster` för att hoppa tillbaka till ursprung position igen.

### *Code outline*

I nedre vänstra hörnet av arbetsytan visas en **OUTLINE** av programmet som är aktivt i editorn. För .p och .w program visas procedurer och funktioner. För klasser visas properties, konstruktor och metoder. Genom att klicka en gång på en rad i **OUTLINE** hoppar fokus till symbolen i koden. Dubbelklicka för att även fokusera cursorn till koden. Listan med **OUTLINE** uppdateras löpande när programmet redigeras, men med en viss fördröjning.

### *Snippets*

För att underlätta kodandet ytterligare finns det ett antal *Snippets* som byter ut det du skrivit mot ett block av kod. Skriv en av nedanstående *Snippets* och tryck `Tab` och koden "vecklar ut sig". En *Snippet* kan bestå av variabler som kan fyllas i. Hoppas med `Tab` för att komma till nästa variabel. Tryck även `Tab` efter att ha fyllt i sista variabeln för att slutföra *Snippeten*.

![Snippet example](images/snippet_example.gif)

Dessa *Snippets* finns definierade och ger följande kod:

#### head

```abl
/**************************************************************************
 * Program:    test.p
 * Beskrivning:
 *
 *
 * Skrivet av:
 * Datum:      2020-02-02
 *
 * �ndringslogg:
 **************************************************************************/
```

**Observera** att "Ä" i Ändringslogg blir fel. Det här beror på att *Snippets* skrivs med en annan encoding än Porgress-koden. Det är bara att ändra det konstaiga tecknet till ett "Ä".

#### def

```abl
define variable myVar as character no-undo.
```

#### dp

```abl
define input parameter varName as character no-undo.
```

#### buf

```abl
define buffer buffer for table.
```

#### ifa

```abl
if available table then
do:

end.
```

#### om

```abl
for each t01objekt no-lock
   where t01objekt.avtalnr = avtalnr
     and t01objekt.kundnr = kundnr,
    each t01moment no-lock
   where t01moment.kundnr = t01objekt.kundnr
     and t01moment.objektnr = t01objekt.objektnr
     and (t01moment.aors = 0 or (t01moment.aors > 0 and t01moment.dattill > today)):

end.
```

#### dso

```abl
define stream utf.
output stream utf to "C:\Code\Progress\Combi\utdata\outputfile.txt".
put stream utf unformatted output skip.
output stream utf close.
```

#### dsi

```abl
define stream inf.
define variable inrad as character no-undo.
input stream inf from "filename".
repeat
    import stream inf unformatted inrad.
    inrad = trim(inrad).
    if inrad <> "" then
    do:

    end.
end.
input stream inf close.
```

#### inp

```abl
input varName as character
```

Den här är bra när man ska lägga till parametrar till functioner och metoder.

#### mb

```abl
message "message" view-as alert-box.
```

#### tt

```abl
define temp-table ttName no-undo
    field fieldName as character.
```

#### ttf

```abl
field fieldName as character.
```

#### proc

```abl
procedure procName:

end procedure.

```

#### func

```abl
function functionName returns character (input parameterName as character):

    return.
end function.
```

### Tabellfunktioner

För att snabbt skriva en tabellkommando så som exempelvis `for each...` eller `find first...` går det att markera ett tabellnamn i koden och trycka `Ctrl`+`Alt`+`T`. Välj tabellkommando så byts tabellnamnet i koden ut mot ett helt kod-uttryck.


Till tabellfunktionen för `for each` kan man lägga till tre parametrar.

* w - Denna ger en where-sats med fälten från tabellens primärindex.
* f - Skapar kod för att skriva en lista med tabellens innehåll till en fil
* b - Lägger till kod för att begränsa resultatet.

Om du exempelvis markerar `T04master,f` och trycker `Ctrl`+`Alt`+`T` och väljer `for each` visas:

```abl
for each T04master no-lock
   where T04master.land = 
     and T04master.datfrom = :
    disp T04master with 2 col.
end.
```

Parametrarna kan också kombineras. Om du exempelvis markerar `T04master,w,f` och trycker `Ctrl`+`Alt`+`T` och väljer `for each` visas:

```abl
define stream utf.
output stream utf to "c:\Code\Progress\Combi\utdata\list_T04master.csv".
put stream utf unformatted "aktiv;basbelop2;basbelop3;basbelopp;belopp;datfrom;divisor;kurs;land;rader;valuta" skip.
for each T04master no-lock
   where T04master.land =
     and T04master.datfrom = :
    put stream utf unformatted
        T04master.aktiv ";"
        T04master.basbelop2 ";"
        T04master.basbelop3 ";"
        T04master.basbelopp ";"
        string(T04master.belopp, "->>>,>>>,>>9.99") ";"
        string(T04master.datfrom, "9999-99-99") ";"
        string(T04master.divisor, ">>>,>>9.99") ";"
        string(T04master.kurs, "->>,>>9.99") ";"
        T04master.land ";"
        T04master.rader ";"
        T04master.valuta skip.
end.
output stream utf close.
```

För att visa information om en tabell, markera tabellens namn (utan parametrar) och tryck `Shift`+`Ctrl`+`Alt`+`T`. Informaitonen visas i nedre delen av skärmen.

![Table information](images/tableinfo.png)

För att visa vilka tabeller som innehåller ett specifikt fält, markera fältnamnet, tryck `Ctrl`+`Alt`+`P` och vält kommandot `LF-Tools: Show tables that contains selected field`. Informaitonen visas i nedre delen av skärmen.

![Tables for field](images/tables_for_field.png)

### *Integration med Progress OpenEdge*

Integrationen är byggd med hjälp av funktioner i Winenv2 för att hämta paramertar och inställningar för vald miljö. Detta är gjort för att inte behöva installera om och göra nya inställningar när en ny miljö skapas eller flyttas.

Alla Progress-kommandon körs mot en förvald Progressmiljö. Som default är PT1 förvald. Det här betyder att kompilering och kör görs i PT1.
Tryck `Ctrl`+`Shift`+`P`och välj kommando **LF-Tools: Select working environment** *(Alla kommandon är på engelska för att VS Code inte klarar av att visa ÅÄÖ i kommandolistan)*. En lista visas då med de miljöer som är tillgängliga. Listan hämtas från Winenv vid start av VS Code. Längst ner i vänstra hörnet på skärmen visas vald miljö.

![Selected environment](images/selectedenv.PNG)

Det går också att klicka på texten *Combi Förvaltning PT1* för att visa listan med valbara miljöer.

![Select environment](images/select-env.gif)

För att göra det enklare att byta till VS Code från Progress-editorn finns de två mest använda kommandona med även i LF-Tools, `F2` för att köra program och `Shift`+`F2` för att kontrollera syntax (kompilera).

#### Kontrollera syntax (kompilera)

När ett program sparas körs en syntax check mot vald miljö. Resultatet syns i nedre vänstra hörnet, bredvid namnet på den valda miljön. Om fel uppstår markeras raden med felet. Kontroll av syntax görs vid spara eller när man trycker `Shift`+`F2`.

![Select environment](images/syntax-check.gif)

#### Kör program

Det finns två sätt att köra program, antingen med `F2` där eventuellt resultat visas i ett Progress-fönster eller genom att trycka `Alt`+`F2` för att visa resultatet direkt i VS Code. **Observera att den senast sparade koden är den som körs. Det betyder att du måste spara innan du kör.** Detta är en skillnad från att köra direkt i Procedure editor. 

Propath kommer alltid peka på den aktuella arbetskatalogen plus den ordinarie propathen för vald miljö. Det här gör att man inte längre är beroende av att alltid utveckla program i C:\Combi för Combi och C:\TureUtv för Ture. Det går att skapa många olika arbetskataloger.

Nedan beskriver hur resultatet visas beroende på hur man kör. Följande kod har använts som exempel:

```abl
for each T01ftextparam no-lock:
    disp objgrp moment momvillk paramid varde format "x(10)".
end.
```

##### Kör via F2

Det aktuella programmet måste vara sparat annars kommer det senast sparade versionen att köras. Tryck sedan `F2` så körs programmet i den valda miljön. Resultatet visas på det här sättet.

![Run with F2](images/run-with-f2.png)

##### Kör via Alt+F2

Genom att köra med `Alt`+`F2` visas resultat direkt i VS Code. Det kan vara bra i de fall men vill kopiera något värde ur resultatet av utsökningen. VS Code stöder tyvärr inte ÅÄÖ i resultatet så dessa visas som konstiga tecken som bilden nedan visar.

![Run with Alt+F2](images/run-with-alt-f2.png)

Om du inte vill fortsätta visa Output-panelen är det bara att trycka `Ctrl`+`J` för att stänga den.

#### Öppna i Progress-editor

Ibland vill man kanske öppna det program man jobbar med i Progress-editorn istället för i VS Code. Det kan man göra genom att spara koden och sedan trycka `F3`. Programmet öppnas då i Progress-editorn och propath är satt till arbetskatalogen plus den ordinarie propathen för vald miljö.

#### Start en Combi- eller Ture-miljö

Klicka på `Ctrl`+`Alt`+`P` för att få upp en lista över valbara miljöer. Miljön startas med propath till den aktuella arbetskatalogen plus den ordinarie propathen för vald miljö.

### Integration med TFS

Integrationen med TFS innehåller än så länge bara två funktioner, jämför program och öppna program.

#### Jämför program

Ibland när man gjort större ändringar i ett program vill man kontrollera skillnaden mot den tidigare versionen för att se att man inte ändrat något man inte borde ha ändrat. Det här är väldigt enkelt i VS Code med LF-Tools.

Ha det aktuella progammet öppet och sparat i VS Code och tryck bara `Ctrl`+`Alt`+`C` så visas ett diff-fönster. Alternativt kan man trycka `Ctrl`+`Shift`+`P` och sedan välja funktionen **LF-Tools: Compare current file with file in source control**.

![Compare programs](images/compare.gif)

#### Öppna program

Om man, som i exemplet nedan, är intresserad av vad programmet ```batprgi.p``` gör kan man ställa markören på progamnamnet och trycka `Ctrl`+`Alt`+`O`. Programmet öppnas då från TFS-katalogen i en egen flik. Man behöver med andra ord inte markera hela programmet, även om det också fungerar.

![Open TFS program](images/open-tfs.gif)

### Alla kommandon i LF-Tools

Här är listan med alla kommandon som idag finns i LF-Tools:

![Multi cursor image](images/lftools_commands.png)

## Inställningar

Inställningar för LF-Tools är lagrade i filen .lftools.config.json som ligger under .lftools i arbetskatalogen.
Filen innehåller inställningar för den aktiulla arbetskatalogen och kan ändras om så önskas.

Så här ser filen ut:

```json
{
    "systemId": "Combi",
    "workingDirectory": "${workspaceFolder}",
    "dlc": "C:\\Progress\\OpenEdge",
    "serverFilterPrefix": "e75lc",
    "progressVersion": "11.7",
    "useLocalDB": false,
    "syntaxCheckMode": "serverenv",
    "usePickListOnStartEnv": true,
    "checkSyntaxOnSave": true,
    "propathMode": "append",
    "propath": [
        "${workspaceFolder}"
    ],
    "we2ServiceProgram": "we2VSCode.p",
    "we2PfFile": "\\\\e75lc0024\\client\\winenv2\\swedish.pf",
    "we2Propath": [
        "\\\\e75lc0024\\client\\winenv2\\sure_r",
        "\\\\e75lc0024\\client\\winenv2"
    ],
    "sourceControlFolder": "C:\\CombiTfs\\src",
    "paramsInOutline": false,
    "includesInOutline": false,
    "selectedEnvId": 999,
    "localDBConfig": {
        "localEnvId": 999,
        "localEnvName": "Lokal Combi",
        "localEnvPfFile": "C:\\LokEnv\\Combi\\winsure\\cwinsure.pf",
        "localEnvIniFile": "C:\\LokEnv\\Combi\\winsure\\proini_vscode.ini",
        "localEnvPropath": [
            "C:\\LokEnv\\Combi\\server\\sure_rb",
            "C:\\LokEnv\\Combi\\server\\sure_src",
            "C:\\LokEnv\\Combi\\client\\sure_r",
            "C:\\LokEnv\\Combi\\client\\sure_src"
        ]
    },
    "debugLogging": false,
    "formatting": {
      "updateCaseOnFormat": true,
      "useUpperCase": true,
      "updateIndent": true,
      "updateStatements": true
    }
}
```

## Kommande funktioner och förbättringar

* Automatisk formatering
* Möjlighet att debugga Progresskod direkt i VS Code
* Utökad integration med TFS, se versionshistorik, öppna ärende direkt från VSCode, mm.
* Förbättringar av IntelliSence, få upp lista med methoder i en klass, mm.

## Kända fel

För tillfället finns det inga kända fel.

## Release Notes

### 0.1.1

Första releasen av LF-Tools extension för VS Code.
