# Versuch 1 - Anwendungsschicht

Zur Lösung dieses Versuchs steht ihnen neben einer virtuelle Maschine seit dem SS22 auch ein Docker-Container 
zur Verfügung. Wir empfehlen ihnen dessen Nutzung, insofern Sie die Aufgaben Vor-Ort an einem Pool-Rechner lösen möchten.
Innerhalb des Docker-Containers befindet sich, ähnlich der virtuellen Maschine, ein Mail-Server der unter anderem den notwendigen Mail Transfer Agent 
Postfix und Mail Delivery Agent Dovecot enthält.
Weitere Informationen zur Einrichtung und Nutzung, finden Sie in `/versuch1-docker/einrichtung.md`.
Sollten Sie die virtuelle Maschine benutzen, können Sie hier direkt fortfahren.

## Anmeldeinformationen und MailDir-Ordner

Benutzername: `labrat`<br>
Passwort: `kn1lab`<br>
MailDir-Ordner: `/home/labrat/Maildir`

## Aufgabe 1

Öffnen Sie die unter `kn1lab/versuch1/beispiel-nachricht.eml` abgelegte Beispiel-Nachricht mit einem Texteditor und erklären Sie grob den Aufbau der Nachricht, sowie die Aufgaben der einzelnen Bestandteile.

## Aufgabe 2

Die zweite Aufgabe umfasst das Senden einer E-Mail mit Hilfe der Java Mail API. Die Dokumentation dazu finden sie auf der Oracle Website unter:

<https://docs.oracle.com/javaee/7/api/javax/mail/package-summary.html>

<https://docs.oracle.com/cd/E26576_01/doc.312/e24930/javamail.htm#GSDVG00079>

Für diese Aufgabe können Sie `kn1lab/versuch1` in IntelliJ öffnen. 
Die Vorlage für diese Aufgabe finden Sie in IntelliJ unter `versuch1/src/Send_Mail.java`.

#### Falls Sie die virtuelle Maschine benutzen
Der Mail-Server läuft auf `localhost`, d.h. die E-Mail-Adressen für Sender und Empfänger müssen auf `@localhost` enden. 
Da es auf dem Rechner (normalerweise) nur den Benutzer `labrat` gibt, sollten Sie die Nachricht an `labrat@localhost` senden. 
Um später erfolgreich eine Sitzung aufzubauen, benötigen Sie nur den Namen des Hosts. Die E-Mail dürfen Sie direkt über den Code erzeugen.

Um zu kontrollieren, ob die E-Mail erfolgreich versendet wurde, kann im Ordner `/home/user/Maildir` im Unterordner `new` nachgeschaut werden. 

#### Falls Sie Docker benutzen
Der Mail-Server läuft auf `localhost`, allerdings müssen die E-Mail-Adressen für Sender und Empfänger auf `@my-hostname` enden.
Die Benutzer sollten Sie während der Einrichtung der Laborumgebung (siehe `/versuch1-docker/einrichtung.md`) schon angelegt haben.
Melden Sie sich unter der Nutzung der Java API mit einem der Benutzer an und Senden Sie eine Nachricht an einen anderen Benutzer.

Um zu kontrollieren, ob die E-Mail erfolgreich versendet wurde, kann im Ordner `/versuch1/versuch1-docker/docker-data/dms/mail-data/<my-hostname>/<my-username>` im Unterordner `new` nachgeschaut werden.

## Aufgabe 3

Die dritte Aufgabe dreht sich darum, alle versendeten E-Mails aus Aufgabe 2 abzurufen. Hierfür ist es völlig ausreichend sie in der Konsole auszugeben. In der Ausgabe sollte enthalten sein:

* Eine Nummerierung die angibt um die wievielte ausgegebene Mail es sich handelt
* Absender der E-Mail
* Der Betreff der E-Mail
* Das Versanddatum der E-Mail
* Der Inhalt der E-Mail

Die Vorlage für diese Aufgabe finden Sie in IntelliJ unter `versuch1/src/Receive_Mail.java`.

Um erfolgreich eine Sitzung aufzubauen, werden der Name des Hosts, dessen Store-Type und die Anmeldeinformationen (siehe ganz oben in diesem Dokument) benötigt.

Zur Erinnerung: es handelt sich um einen POP3-Server mit unverschlüsselter Verbindung.

Bei Problemen können die folgenden Parameter gesetzt werden:

```java
properties.put("mail.debug", "true");
properties.put("mail.debug.quote", "true");
session.setDebug(true);
```

Hilfreich ist auch:

```bash
tail -f /var/log/mail.log
```
