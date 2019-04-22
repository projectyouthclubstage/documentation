# Bestandteile und Technologien der Anmeldung

## Authentifizierung mit OpenId

Um die Authentifzierung sicherzustellen werden die externen Auth-Provider von 
Google[^google] und Facebook[^facebook] verwendet.
Hierbei wird über ein `POST` per *spring-security* automatisch ein Call gegen 
die vorgegebene API des ausgewählten Providers gefahren.

Für Google ist zu beachten, dass die Resource, von der der POST ausgeführt wird, 
direkt beim Erstellen der Auth-API bei Google angegeben werden muss,
incl. Port. Daher müssen hier Änderungen durchgeführt werden, wenn die Anwendung
auf einem neuen Port gestartet werden soll.

Google benötigt eine eigene Konfiguration, während Facebook mit den von Spring
gelieferten Einstellungen funktionsfähig ist.

Der Facebook-Provider gestattet keinen Zugriff auf Daten, die mit *bio* 
abgerufen wrden. Das Erhöhen der Version löst dieses Problem.


## Authentifizierung gegen eigene Daten

Nachdem durch den externen Auth-Provider ein (positives) Ergebnis zurück 
geliefert wurde, wird gegen eigene Daten validiert, ob der Benutzer vorhanden
ist.

Dabei gilt die Kombination aus Provider (Facebook / Google) und die durch den 
Provider gelieferte ID als einmalig und muss direkt in eine Benutzer-ID des
internen Systems übersetzt werden. Anhand diesem Benutzer finden dann die 
Autorisierung und die weitere Kommunikation im System statt. 
Es ist erlaubt, einem Benutzer mehrere Authentifizierungsmöglichkeiten 
zuzuordnen. Kann für eine extern authentifizierte Person kein Benutzer gefunden
werden, so ist sie zwar authentifiziert, aber nicht im System gültig. Es wird
in diesem Fall zur Registrierung weiterverwiesen.


## Autorisierung über den internen Benutzer

Der über die externe und interne Authentifizierung bestätigte Benutzer wird 
einem Kontext - daher eine Organisation zugeordnet. Der zur Authorisierung
auszustellende JWT[^a] ist immer nur innerhalb einer Organisation gültig. Ist
ein Benutzer in mehreren Organisationen gültig, können unterschiedliche 
Tokens nach Auswahl durch den Benutzer ausgestellt werden.

Innerhalb einer Organisation kann ein Benutzer mehereren Gruppen zugeordnet sein
und ein Administrator-Flag gesetzt haben. Administratoren, Moderatoren und 
Systemadministratoren bildern die grobgranulare Authorisierung, die über den 
zentralen Service kommuniziert wird.
Feingranulare Authorisierung nehmen einzelne Services anhand der 
Gruppenzugehörigkeit eines Benutzers vor. 

Administratoren sind berechtigt, Gruppen zu erstellen, Gruppen in einzelnen
Services den Rechten zuzuordnen und andere Administratoren zu ernnenen.
Moderatoren sind berechtigt, Mitglieder der Organisation einzuladen, anzunehmen 
und zu entfernen sowie ihre Zugehörtigkeit zu bestehenden Gruppen zu bearbeiten.

Die Informationen über Gruppenzugehörtigkeit, System-, Administrator und 
Moderator werden in einem JWT gesammelt und so an weitere Services übermittelt.
Dabei wird durch über public- und privat-Keys[^asym] sichergestellt, dass die Daten 
von dem echten Auth-Service gestellt werden.



---
## Links

[^google]: [Google OpenID Connect](https://developers.google.com/identity/protocols/OpenIDConnect)
[^facebook]: [Facebook Login](https://developers.facebook.com/docs/facebook-login/)
[^a]: [JSON Web Token](https://de.wikipedia.org/wiki/JSON_Web_Token)
[^asym]: [Asymmetrische Verschlüsselung](https://de.wikipedia.org/wiki/Asymmetrisches_Kryptosystem)


