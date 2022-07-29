# Anleitung für das dritte Praktikum
**Einführung in den Compilerbau, Wintersemester 2021/22**

## Voraussetzungen

* Eine Java-1.8-kompatible virtuelle Maschine.

## Einrichtung

Für die **Ersteinrichtung** benötigen Sie eine Internetverbindung.

Dieses Projekt verwendet [Gradle 6.6](https://docs.gradle.org/6.6.1/userguide/userguide.html) als Buildwerkzeug. Falls Gradle nicht auf Ihrem System verfügbar ist, können Sie die "Gradle Wrapper" genannten Skripte `gradlew` (Linux und macOS) bzw. `gradlew.bat` (Windows) anstelle des hier in der Anleitung verwendeten `gradle`-Befehls verwenden.

Führen Sie bitte folgendes Kommando aus:

	$ gradle mavlc mtam
	
Falls Sie den Gradle Wrapper benutzen wollen, würden Sie stattdessen folgendes Kommando verwenden:

	$ ./gradlew mavlc mtam

Dies erstellt im Verzeichnis `build/` die Startskripte `mavlc` für den MAVL Compiler Driver sowie `mtam` für den interaktiven Interpreter.

Wenn Sie Eclipse zur Entwicklung verwenden möchten, können Sie mittels

	$ gradle eclipse

ein Eclipse-Projekt erzeugen, welches Sie anschließend in einen beliebigen Eclipse-Workspace importieren können.

## Entwickeln und Testen

Während der Entwicklung können Sie die Übersetzung der Quellen mit

    $ gradle classes

starten. Dies übersetzt nur die geänderten Klassen. Wenn Sie eine komplette Neuübersetzung anstoßen möchten, führen Sie zunächst diesen Befehl aus:

	$ gradle clean

Das Projekt enthält die öffentliche Testfälle der Praktikumsaufgaben, die Sie mittels

	$ gradle test

ausführen können. Das Kommando gibt nur eine Zusammenfassung auf der Konsole aus; den detaillierten Testreport finden Sie in der Datei `build/reports/tests/test/index.html`.

## Abgabe

Mit

	$ gradle prepareSubmission -PGroupNumber=??

erstellen Sie ein Archiv, welches Sie anschließend über den Moodle-Kurs abgeben können. Ersetzen Sie dabei ?? durch Ihre Gruppennummer.

## Compiler Driver

Um den Compiler auszuführen, nutzen Sie das zu Beginn generierte Startscript (siehe oben). Mit 

	$ build/mavlc --help

erhalten Sie eine Liste aller Optionen, mit denen Sie das Verhalten des Compilers steuern können.  
Beachten Sie, dass einige dieser Optionen erst in den späteren Praktika nutzbar sind.

Um beispielsweise ein MAVL Progamm auszuführen und den Output ausgeben zu lassen, nutzen Sie den Befehl

	$ build/mavlc helloworld.mavl --dump-output

### Interpreter ###

Mit Version 2019.1 wird im Wintersemester 2019/20 erstmals der neue interaktive Interpreter mit ausgeliefert.  
Diesen können Sie nutzen, um die generierten Programme Schritt für Schritt zu debuggen.

Um den Interpreter verwenden zu können, müssen Sie zunächst ein MAVL Programm in ein binäres .tam Programmabbild übersetzen.  
Nutzen Sie dafür den Befehl

    $ build/mavlc helloworld.mavl --dump-image --dump-symbols

Die Option `--dump-symbols` spezifiziert dabei, dass die während der Codegenerierung erzeugten Debug-Informationen mit ausgegeben werden sollen.  
Danach können Sie den interaktiven Interpreter mittels

    $ build/mtam

starten. Sie werden dann gebeten, den Pfad zu Ihrer Abbilddatei einzugeben und eventuell gefragt, ob Sie die Debug-Informationen laden möchten.
Alternativ können Sie auch direkt den Pfad zu einer MAVL Sourcedatei angeben, diese wird dann automatisch übersetzt.

Für weitere Informationen zur Bedienung des interaktiven Interpreters sehen Sie sich die Dokumente manual_mtam.pdf sowie spec_mtam.pdf aus dem Moodle-Kurs an.  

## Bekannte Probleme

* Unter Windows funktioniert das Startskript `mavlc.bat` nicht, wenn der Projektpfad nicht-ASCII-Zeichen (also insbesondere Umlaute) enthält.
