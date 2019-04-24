# Registrierung, Anmeldung und Abmeldung

## Anmeldung

Die Anmeldung geschieht in zwei Teilen.

### Kontextfreie Anmeldung

Zunächst authentifiziert sich der Benutzer extern und intern. Gelingt diese 
Authentifizierung werden ihm grundlegende Rechte ausgestellt und Kontext-freie
Eigenschaften wie System-Administrator gegeben.

#### Sequenzdiagram
![Sequenzdiagram der kontextfreien Anmeldung](img/login_without_context.png)

