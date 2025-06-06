## Oppskrift på hvordan man kan hente ned og blokkere IOC'er fra blokklist i Fortigate brannmurer.

Fortigate kan importere eksterne threat feeds for blokkering av IP-addresser, dette gjøres via fanen Security Fabric --> External Connectors.

Create new --> IP Address

Status: Enabled.
Name: settes til noe lett gjenkjennelig.
Update method: Extarnal Feed.
URL of external resources: her brukes IP-cidr filter fra link: https://blocklist.helsecert.no/v3?apikey=<api-nøkkel mottatt på mail>&format=list_cidr&type=ipv4&type=ipv4_cidr
Refresh rate: 5

Så er det og sette en deny policy for addressene det gjelder som blokkerer både utgående og inkommende trafikk fra disse.

-----------------------------------

Deretter lager man en Fortiguard Category for blokking av domener. 

Global --> Security Fabric --> Fabric Connectors.

Klikk på Create new i Threat Feeds seksjonen så velger man FortiGuard Category.

Status: Enabled.
Name: settes til noe lett gjenkjennelig. (eksempelvis HelseCERT domain block)
Update method : External Feed
URL of external resources: https://blocklist.helsecert.no/v3?apikey=<api-nøkkel mottatt på mail>&format=list&type=domain
Refresh rate: 5

Da kan man blokkere denne kategorien ved hjelp av et web filter.
Security Profiles --> Web Filter.

Name : settes til noe lett gjenkjennelig
Feature set : Flow-based

Så trykker man inn på Fortiguard Category Based Filter --> Remote Categories.
Der skal man finne blokkerings kategorien med navn som ble laget i steget over, og så blokkere all trafikk mot disse domenene.
