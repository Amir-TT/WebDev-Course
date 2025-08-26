<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "c63675cfaf1d223b37bb9fecbfe7c252",
  "translation_date": "2025-08-24T12:58:43+00:00",
  "source_file": "1-getting-started-lessons/1-intro-to-programming-languages/README.md",
  "language_code": "de"
}
-->
# Einführung in Programmiersprachen und Werkzeuge des Handwerks

Diese Lektion behandelt die Grundlagen von Programmiersprachen. Die hier behandelten Themen gelten für die meisten modernen Programmiersprachen. Im Abschnitt "Werkzeuge des Handwerks" lernst du nützliche Software kennen, die dir als Entwickler:in hilft.

![Intro Programmierung](../../../../sketchnotes/webdev101-programming.png)
> Sketchnote von [Tomomi Imura](https://twitter.com/girlie_mac)

## Quiz vor der Vorlesung
[Quiz vor der Vorlesung](https://forms.office.com/r/dru4TE0U9n?origin=lprLink)

## Einführung

In dieser Lektion behandeln wir:

- Was ist Programmieren?
- Arten von Programmiersprachen
- Grundelemente eines Programms
- Nützliche Software und Werkzeuge für professionelle Entwickler:innen

> Du kannst diese Lektion auf [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101/introduction-programming/?WT.mc_id=academic-77807-sagibbon) absolvieren!

## Was ist Programmieren?

Programmieren (auch bekannt als Codieren) ist der Prozess, Anweisungen für ein Gerät wie einen Computer oder ein mobiles Gerät zu schreiben. Wir schreiben diese Anweisungen mit einer Programmiersprache, die dann vom Gerät interpretiert wird. Diese Anweisungen können verschiedene Namen haben, aber *Programm*, *Computerprogramm*, *Anwendung (App)* und *ausführbare Datei* sind einige gängige Bezeichnungen.

Ein *Programm* kann alles sein, was mit Code geschrieben wurde; Websites, Spiele und Handy-Apps sind Programme. Auch wenn es möglich ist, ein Programm ohne Code zu erstellen, wird die zugrunde liegende Logik vom Gerät interpretiert, und diese Logik wurde höchstwahrscheinlich mit Code geschrieben. Ein Programm, das *läuft* oder *ausgeführt* wird, führt Anweisungen aus. Das Gerät, mit dem du diese Lektion liest, führt ein Programm aus, um sie auf deinem Bildschirm anzuzeigen.

✅ Recherchiere ein wenig: Wer gilt als der/die erste Computerprogrammierer:in der Welt?

## Programmiersprachen

Programmiersprachen ermöglichen es Entwickler:innen, Anweisungen für ein Gerät zu schreiben. Geräte können nur Binärcode (1en und 0en) verstehen, und für *die meisten* Entwickler:innen ist das keine sehr effiziente Art der Kommunikation. Programmiersprachen sind das Mittel zur Kommunikation zwischen Menschen und Computern.

Programmiersprachen gibt es in verschiedenen Formaten und sie können unterschiedlichen Zwecken dienen. Zum Beispiel wird JavaScript hauptsächlich für Webanwendungen verwendet, während Bash hauptsächlich für Betriebssysteme genutzt wird.

*Low-Level-Sprachen* erfordern in der Regel weniger Schritte als *High-Level-Sprachen*, damit ein Gerät Anweisungen interpretieren kann. Was High-Level-Sprachen jedoch beliebt macht, ist ihre Lesbarkeit und Unterstützung. JavaScript gilt als High-Level-Sprache.

Der folgende Code zeigt den Unterschied zwischen einer High-Level-Sprache wie JavaScript und einer Low-Level-Sprache wie ARM-Assemblercode.

```javascript
let number = 10
let n1 = 0, n2 = 1, nextTerm;

for (let i = 1; i <= number; i++) {
    console.log(n1);
    nextTerm = n1 + n2;
    n1 = n2;
    n2 = nextTerm;
}
```

```c
 area ascen,code,readonly
 entry
 code32
 adr r0,thumb+1
 bx r0
 code16
thumb
 mov r0,#00
 sub r0,r0,#01
 mov r1,#01
 mov r4,#10
 ldr r2,=0x40000000
back add r0,r1
 str r0,[r2]
 add r2,#04
 mov r3,r0
 mov r0,r1
 mov r1,r3
 sub r4,#01
 cmp r4,#00
 bne back
 end
```

Glaub es oder nicht, *sie tun beide dasselbe*: Sie geben eine Fibonacci-Sequenz bis 10 aus.

✅ Eine Fibonacci-Sequenz wird [definiert](https://en.wikipedia.org/wiki/Fibonacci_number) als eine Reihe von Zahlen, bei der jede Zahl die Summe der beiden vorhergehenden ist, beginnend mit 0 und 1. Die ersten 10 Zahlen der Fibonacci-Sequenz sind 0, 1, 1, 2, 3, 5, 8, 13, 21 und 34.

## Elemente eines Programms

Eine einzelne Anweisung in einem Programm wird als *Statement* bezeichnet und hat normalerweise ein Zeichen oder einen Zeilenabstand, der markiert, wo die Anweisung endet oder *terminiert*. Wie ein Programm terminiert, variiert je nach Sprache.

Anweisungen in einem Programm können von Daten abhängen, die von einem Benutzer oder einer anderen Quelle bereitgestellt werden, um Anweisungen auszuführen. Daten können beeinflussen, wie sich ein Programm verhält, daher bieten Programmiersprachen eine Möglichkeit, Daten vorübergehend zu speichern, damit sie später verwendet werden können. Diese werden als *Variablen* bezeichnet. Variablen sind Anweisungen, die ein Gerät anweisen, Daten im Speicher zu speichern. Variablen in Programmen ähneln Variablen in der Algebra, da sie einen eindeutigen Namen haben und sich ihr Wert im Laufe der Zeit ändern kann.

Es besteht die Möglichkeit, dass einige Anweisungen von einem Gerät nicht ausgeführt werden. Dies geschieht in der Regel absichtlich, wenn es vom Entwickler so geschrieben wurde, oder versehentlich, wenn ein unerwarteter Fehler auftritt. Diese Art der Kontrolle über eine Anwendung macht sie robuster und wartbarer. Typischerweise treten diese Kontrolländerungen auf, wenn bestimmte Bedingungen erfüllt sind. Eine gängige Anweisung in modernen Programmiersprachen, um zu steuern, wie ein Programm ausgeführt wird, ist die `if..else`-Anweisung.

✅ Du wirst mehr über diese Art von Anweisungen in späteren Lektionen lernen.

## Werkzeuge des Handwerks

[![Werkzeuge des Handwerks](https://img.youtube.com/vi/69WJeXGBdxg/0.jpg)](https://youtube.com/watch?v=69WJeXGBdxg "Werkzeuge des Handwerks")

> 🎥 Klicke auf das Bild oben, um ein Video über Werkzeuge anzusehen

In diesem Abschnitt lernst du einige Software kennen, die du als nützlich empfinden könntest, wenn du deine Reise als professionelle:r Entwickler:in beginnst.

Eine **Entwicklungsumgebung** ist eine einzigartige Sammlung von Werkzeugen und Funktionen, die ein:e Entwickler:in häufig beim Schreiben von Software verwendet. Einige dieser Werkzeuge wurden speziell auf die Bedürfnisse eines:einer Entwickler:in zugeschnitten und können sich im Laufe der Zeit ändern, wenn sich die Prioritäten in der Arbeit, bei persönlichen Projekten oder bei der Verwendung einer anderen Programmiersprache ändern. Entwicklungsumgebungen sind so einzigartig wie die Entwickler:innen, die sie nutzen.

### Editoren

Eines der wichtigsten Werkzeuge für die Softwareentwicklung ist der Editor. Editoren sind der Ort, an dem du deinen Code schreibst und manchmal auch ausführst.

Entwickler:innen verlassen sich aus mehreren Gründen auf Editoren:

- *Debugging* hilft, Fehler und Probleme aufzudecken, indem der Code Zeile für Zeile durchgegangen wird. Einige Editoren verfügen über Debugging-Funktionen, die für bestimmte Programmiersprachen angepasst und hinzugefügt werden können.
- *Syntaxhervorhebung* fügt Farben und Textformatierungen zum Code hinzu, was ihn leichter lesbar macht. Die meisten Editoren erlauben eine angepasste Syntaxhervorhebung.
- *Erweiterungen und Integrationen* sind spezialisierte Werkzeuge für Entwickler:innen, die von anderen Entwickler:innen erstellt wurden. Diese Werkzeuge sind nicht im Basis-Editor enthalten. Zum Beispiel dokumentieren viele Entwickler:innen ihren Code, um zu erklären, wie er funktioniert. Sie könnten eine Rechtschreibprüfungserweiterung installieren, um Tippfehler in der Dokumentation zu finden. Die meisten Erweiterungen sind für die Verwendung in einem bestimmten Editor gedacht, und die meisten Editoren bieten eine Möglichkeit, nach verfügbaren Erweiterungen zu suchen.
- *Anpassung* ermöglicht es Entwickler:innen, eine einzigartige Entwicklungsumgebung zu schaffen, die ihren Bedürfnissen entspricht. Die meisten Editoren sind extrem anpassbar und erlauben es Entwickler:innen, eigene Erweiterungen zu erstellen.

#### Beliebte Editoren und Webentwicklungs-Erweiterungen

- [Visual Studio Code](https://code.visualstudio.com/?WT.mc_id=academic-77807-sagibbon)
  - [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)
  - [Live Share](https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare)
  - [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
- [Atom](https://atom.io/)
  - [spell-check](https://atom.io/packages/spell-check)
  - [teletype](https://atom.io/packages/teletype)
  - [atom-beautify](https://atom.io/packages/atom-beautify)
  
- [Sublimetext](https://www.sublimetext.com/)
  - [emmet](https://emmet.io/)
  - [SublimeLinter](http://www.sublimelinter.com/en/stable/)

### Browser

Ein weiteres wichtiges Werkzeug ist der Browser. Webentwickler:innen verlassen sich auf den Browser, um zu sehen, wie ihr Code im Web ausgeführt wird. Er wird auch verwendet, um die visuellen Elemente einer Webseite anzuzeigen, die im Editor geschrieben wurden, wie HTML.

Viele Browser verfügen über *Entwicklerwerkzeuge* (DevTools), die eine Reihe hilfreicher Funktionen und Informationen enthalten, um Entwickler:innen dabei zu helfen, wichtige Informationen über ihre Anwendung zu sammeln und zu erfassen. Zum Beispiel: Wenn eine Webseite Fehler hat, ist es manchmal hilfreich zu wissen, wann sie aufgetreten sind. DevTools in einem Browser können so konfiguriert werden, dass diese Informationen erfasst werden.

#### Beliebte Browser und DevTools

- [Edge](https://docs.microsoft.com/microsoft-edge/devtools-guide-chromium/?WT.mc_id=academic-77807-sagibbon)
- [Chrome](https://developers.google.com/web/tools/chrome-devtools/)
- [Firefox](https://developer.mozilla.org/docs/Tools)

### Kommandozeilenwerkzeuge

Einige Entwickler:innen bevorzugen eine weniger grafische Ansicht für ihre täglichen Aufgaben und verlassen sich auf die Kommandozeile, um dies zu erreichen. Das Schreiben von Code erfordert eine erhebliche Menge an Tippen, und einige Entwickler:innen bevorzugen es, ihren Arbeitsfluss auf der Tastatur nicht zu unterbrechen. Sie verwenden Tastenkombinationen, um zwischen Desktop-Fenstern zu wechseln, an verschiedenen Dateien zu arbeiten und Werkzeuge zu nutzen. Die meisten Aufgaben können mit einer Maus erledigt werden, aber ein Vorteil der Kommandozeile ist, dass vieles mit Kommandozeilenwerkzeugen erledigt werden kann, ohne zwischen Maus und Tastatur wechseln zu müssen. Ein weiterer Vorteil der Kommandozeile ist, dass sie konfigurierbar ist und du eine benutzerdefinierte Konfiguration speichern, später ändern und auf andere Entwicklungsmaschinen importieren kannst. Da Entwicklungsumgebungen so einzigartig für jede:n Entwickler:in sind, vermeiden einige die Kommandozeile, andere verlassen sich vollständig darauf, und wieder andere bevorzugen eine Mischung aus beidem.

### Beliebte Kommandozeilenoptionen

Die Optionen für die Kommandozeile unterscheiden sich je nach Betriebssystem.

*💻 = ist standardmäßig auf dem Betriebssystem vorinstalliert.*

#### Windows

- [Powershell](https://docs.microsoft.com/powershell/scripting/overview?view=powershell-7/?WT.mc_id=academic-77807-sagibbon) 💻
- [Command Line](https://docs.microsoft.com/windows-server/administration/windows-commands/windows-commands/?WT.mc_id=academic-77807-sagibbon) (auch bekannt als CMD) 💻
- [Windows Terminal](https://docs.microsoft.com/windows/terminal/?WT.mc_id=academic-77807-sagibbon)
- [mintty](https://mintty.github.io/)
  
#### MacOS

- [Terminal](https://support.apple.com/guide/terminal/open-or-quit-terminal-apd5265185d-f365-44cb-8b09-71a064a42125/mac) 💻
- [iTerm](https://iterm2.com/)
- [Powershell](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-7/?WT.mc_id=academic-77807-sagibbon)

#### Linux

- [Bash](https://www.gnu.org/software/bash/manual/html_node/index.html) 💻
- [KDE Konsole](https://docs.kde.org/trunk5/en/konsole/konsole/index.html)
- [Powershell](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-7/?WT.mc_id=academic-77807-sagibbon)

#### Beliebte Kommandozeilenwerkzeuge

- [Git](https://git-scm.com/) (💻 auf den meisten Betriebssystemen)
- [NPM](https://www.npmjs.com/)
- [Yarn](https://classic.yarnpkg.com/en/docs/cli/)

### Dokumentation

Wenn ein:e Entwickler:in etwas Neues lernen möchte, wird er:sie sich höchstwahrscheinlich an die Dokumentation wenden, um zu erfahren, wie man es benutzt. Entwickler:innen verlassen sich oft auf Dokumentationen, um sich darüber zu informieren, wie Werkzeuge und Sprachen richtig verwendet werden, und um ein tieferes Verständnis dafür zu erlangen, wie sie funktionieren.

#### Beliebte Dokumentationen zur Webentwicklung

- [Mozilla Developer Network (MDN)](https://developer.mozilla.org/docs/Web), von Mozilla, den Herausgebern des [Firefox](https://www.mozilla.org/firefox/)-Browsers
- [Frontend Masters](https://frontendmasters.com/learn/)
- [Web.dev](https://web.dev), von Google, den Herausgebern von [Chrome](https://www.google.com/chrome/)
- [Microsofts eigene Entwicklerdokumentation](https://docs.microsoft.com/microsoft-edge/#microsoft-edge-for-developers), für [Microsoft Edge](https://www.microsoft.com/edge)
- [W3 Schools](https://www.w3schools.com/where_to_start.asp)

✅ Recherchiere: Jetzt, da du die Grundlagen der Umgebung eines Webentwicklers kennst, vergleiche sie mit der Umgebung eines Webdesigners.

---

## 🚀 Herausforderung

Vergleiche einige Programmiersprachen. Was sind einige der einzigartigen Merkmale von JavaScript im Vergleich zu Java? Wie sieht es mit COBOL im Vergleich zu Go aus?

## Quiz nach der Vorlesung
[Quiz nach der Vorlesung](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/2)

## Wiederholung & Selbststudium

Lerne ein wenig über die verschiedenen Programmiersprachen, die einem Programmierer zur Verfügung stehen. Versuche, eine Zeile in einer Sprache zu schreiben, und schreibe sie dann in zwei anderen Sprachen um. Was hast du dabei gelernt?

## Aufgabe

[Die Dokumentation lesen](assignment.md)

**Haftungsausschluss**:  
Dieses Dokument wurde mit dem KI-Übersetzungsdienst [Co-op Translator](https://github.com/Azure/co-op-translator) übersetzt. Obwohl wir uns um Genauigkeit bemühen, beachten Sie bitte, dass automatisierte Übersetzungen Fehler oder Ungenauigkeiten enthalten können. Das Originaldokument in seiner ursprünglichen Sprache sollte als maßgebliche Quelle betrachtet werden. Für kritische Informationen wird eine professionelle menschliche Übersetzung empfohlen. Wir übernehmen keine Haftung für Missverständnisse oder Fehlinterpretationen, die sich aus der Nutzung dieser Übersetzung ergeben.