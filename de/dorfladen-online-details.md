---
parent: Dorfladen Online
title: Details
nav_order: 1
---

# Details zu den Abläufen bei Dorfladen Online

* Die Kunden-Rechnungen werden automatisch jeden Samstag um 10:00 Uhr (Zeitpunkt änderbar) erstellt und per E-Mail an die Kunden versendet. Das Erstellen einer Rechnung kann aber auch manuell ausgelöst werden (z.B. für Laufkundschaft). Diese manuell generierten Rechnungen können auch als "bar bezahlt" markiert werden.

* Beim Erstellen einer Rechnung oder dem Anzeigen der Rechnungs-Vorschau werden immer alle Bestellungen **des aktuellen Tages** und von **bereits vergangenen Tagen** verwendet, aber **niemals die Daten von noch offenen, zukünftigen Vorbestellungen**. Das Auswählen von bestimmten bestellten Produkten für die Rechnung ist also nicht möglich.

* Der Umsatzsteuersatz von Pfand wird über die sogenannte "Vereinfachungsregel" abgebildet: dh. **immer 20% USt.** (unabhängig vom Steuersatz des eigentlichen Produktes).

* Die erstellten Rechnungen werden übersichtlich im **Journal** (zu finden unter "Finanzberichte / Journal") zusammengefasst. Die Rechnungsummen werden auch nach Umsatzsteuer gruppiert dargestellt, das erleichtert die Buchhaltung.

* Auch das Stornieren von Rechnungen ist rechtlich korrekt umgesetzt, es wird dafür eine Storno-Rechnung mit den Negativ-Beträgen der Original-Rechnung erstellt.

* Erfassung des Einkaufspreises als Daten-Grundlage zur Gewinnermittlung.
* [Schnittstelle zu Registrierkasse HelloCash (hellocash.at)]({{ site.baseurl }}/de/dorfladen-online-registrierkasse-hello-cash.html)

* Für Kunden-Rechnungen kann nun ein Prefix (max. 6 Zeichen) angegeben werden. Achtung: Nicht möglich bei Verwendung der Hello-Cash-API!

### Automatischer Rechnungsdruck
Im Selbstbedienungs-Modus wird die Rechnung automatisch erstellt und gedruckt, wenn der Kunde entweder bar bezahlt (Laufkunde) oder den Rechnungsversand deaktiviert hat. Für Laufkundschaft am Besten einen Kunden mit der neuen User-Gruppe "SB-Kunde" verwenden **und den Rechnungsversand bei diesem Kunden deaktiveren**.

Mit `app.selfServiceModeAutoGenerateInvoice => false` kann die automatische Rechnungserstellung im SB-Modus ausgestellt werden.

* Für das Bar-Bezahlen von Vorbestellungen gilt für den automatischen Rechnungsdruck die gleiche Logik.

* Automatisches Drucken im Hintergrund aktivieren: **Firefox:** about:config / print.always_print_silent: true
**Chrome:** [Anleitung](https://help.brightpearl.com/hc/en-us/articles/360028542572-Chrome-settings-for-silent-printing)

{: .new }
Der Betreiber wird jetzt mit eine E-Mail benachrichtigt, falls ein Bestell-Kommentar verfasst wurde.