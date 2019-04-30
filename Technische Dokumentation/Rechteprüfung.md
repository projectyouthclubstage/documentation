# Grundlagen der Rechteprüfung

## Grobgranulare Rechteprüfung

Die grobgranulare Rechteprüfung findet anhand von Flags statt, die im 
Authorisierungs-Token mit bei der Anmeldung ausgestellt werden.

Dabei stehen folgende Rollen zur Verfügung:

### System-Administrator

Die Rolle des System-Administrators ist unabhängig von Kontext, bzw.
Organisation. 

System-Administratoren sind berechtigt, neue Benutzer in das 
System einzufügen, sie zu sperren oder zu löschen,.

### Administrator

Die Rolle des Administrator ist immer nur im Rahmen einer Organisation gültig.
Ein Benutzer kann Administrator mehrere Organisationen sein, muss aber zwischen
diesen aktiv wechseln. 
Erstellt ein Benutzer eine Organisation, so ist er automatisch Administrator in
dieser Organisation.
Ist ein Benutzer Administrator oder wird zum Administrator gemacht, so ist er
automatisch auch Moderator. Die Moderatoren-Rolle kann ihm erst entzogen werden,
wenn er auch kein Administrator mehr ist.

Administratoren sind berechtigt, Gruppen anzulegen und zu löschen, den Gruppen
Rechte-Funktionen zuzuweisen, sowie neue Administratoren und Moderatoren zu 
ernennen.

### Moderator

Die Rolle des Moderator ist immer nur im Rahmen einer Organisation gültig.
Ein Benutzer kann Moderator mehrere Organisationen sein, muss aber zwischen
diesen aktiv wechseln. 
Die Moderatoren-Rolle wird bei der Vergabe von Administrator-Rechten automatisch
angelegt, beim Entfernen allerdings nicht mit gelöscht.
Das Löschen der Moderatoren-Rolle muss bewusst im Nachgang erledigt werden. Ein
Benutzer, der Administrator ist, ist immer auch Moderator.

Administratoren sind berechtigt, Benutzer in die Organisation einzuladen, 
aufzuhemen und zu löschen. Außderdem dürfen sie Zuordnungen von Gruppen und
Mitgliedern bearbeiten.

### Mitglied

Jeder Benutzer, der Teil einer Organisation ist, ist Mitglied dieser 
Organisation und hat dementsprechenden Zugriff auf Informationen der 
Organisation, wenn diese nicht durch spezielle Rollen-Gruppen abgesichert sind.

## Feingranulare Rechteprüfung

Die feingranulare Rechteprüfung findet anhand der Gruppenzugehörigkeiten des
Benutzers statt, die im Authorisierungs-Token mitgeliefert werden.

Welche Gruppe dabei welchem Recht zugeordnet ist, entscheidet der Administrator
durch Zuordnung im entsprechenden Dienst. Die Authorisierung übernimmt ein 
Service des Diensts ohne Kommunikation mit einem zentralen Rechteprovider.