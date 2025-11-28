# Coolbx Ansible Configuration

Dit project bevat de Ansible configuratie voor het beheren van laptops binnen de schoolomgeving. Het zorgt voor de installatie van software, configuratie van instellingen en het toepassen van specifieke regels op basis van de gebruikersgroep (leerlingen, leerkrachten, administratie).

## Vereisten

Om dit playbook uit te voeren, moet Ansible geïnstalleerd zijn op de machine. Daarnaast is er een specifiek bestand nodig om de laptop te identificeren:

-   **Bestand:** `/usr/share/ansible/laptop-group`
-   **Inhoud:** De naam van de groep waartoe de laptop behoort.
    -   `leerlingen`
    -   `leerkrachten`
    -   `administratie`

Als dit bestand niet bestaat of leeg is, worden alleen de algemene taken uitgevoerd.

## Gebruik

Om de configuratie toe te passen op de lokale machine, voer je het volgende commando uit vanuit de root van dit project:

```bash
ansible-playbook local.yml
```

## Configuratie Details

Het `local.yml` playbook bepaalt eerst de laptopgroep en voert vervolgens de relevante taken uit.

### Algemeen (`playbooks/common.yml`)
Deze taken worden op **alle** laptops uitgevoerd:
-   Toevoegen van de Flathub remote.
-   Configuratie van de netwerkprinter "HP_M406_School" (indien niet aanwezig).
-   Installatie van Firefox (via Flatpak).
-   Installatie van VLC (via Flatpak).

### Leerlingen (`playbooks/lln.yml`)
Specifiek voor laptops van leerlingen:
-   Installatie van GIMP.
-   Verwijderen van Steam (indien aanwezig).
-   Instellen van window button layout (minimize, maximize, close).
-   Downloaden en instellen van een specifieke bureaubladachtergrond van Unsplash (ook voor dark mode).

### Leerkrachten (`playbooks/lkn.yml`)
Specifiek voor laptops van leerkrachten:
-   Installatie van VSCodium.

### Administratie (`playbooks/admin.yml`)
Specifiek voor laptops van de administratie:
-   Momenteel zijn er nog geen specifieke taken gedefinieerd (placeholder).