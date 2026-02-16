# ansible-roles-elastic

# elastic-agents

## Installazione elasti agents

Playbook dedicato all'installazione dell'elastic agent su tutti gli host compatibili.

Il playbook richiama 3 ruoli:

* `install_agent_linux`: installa l'agente su host con os Linux (Debian e RedHat)
* `install_fleet_server`: installa l'agente su host con os Linux (Debian e RedHat)
* `install_agent_windows`: installa l'agente su host con os Windows

Gli host windows e linux devono essere gestiti nell'inventory con appositi gruppi.

Per i ruoli install_agent_linux e install_agent_windows è necessario configurare le seguenti variabili:

* `elastic_agent_version`: versione dell'agente da installare (deve essere la stessa di elasticsearch)
* `fleet_server_url`: url per connettersi al fleet server (componente elastic per la gestione centralizzata degli agent)
* `enrollment_token`: token da utilizzare per connettersi al fleet server. Da definire nel vault
* `install_dir`: directory di installazione. Facoltativa in quanto già settata di default all'interno del ruolo

Per l'installazione del fleet server sono da configurare le seguenti variabili:

* `elastic_agent_version`: versione dell'agente da installare (deve essere la stessa di elasticsearch)
* `elastic_url`: url per connettersi a elasticsearch 
* `fleet_server_service_token`: token da utilizzare per l'installazione del fleet server. Da definire nel vault
* `install_dir`: directory di installazione. Facoltativa in quanto già settata di default all'interno del ruolo
* `fleet_server_policy`: Policy da utilizzare per l'installazione del fleet server. Facoltativa in quanto già settata di default all'interno del ruolo
* `fleet_server_port`: Porta in ascolto sul fleet server. Facoltativa in quanto già settata di default all'interno del ruolo
* `insecure`: booleano, definisce se utilizzare la modalita' insecure (comunicazione con elasticsearch senza verifica del certificato). Facoltativa in quanto già settata di default a False all'interno del ruolo
* `fleet_server_es_ca_trusted_fingerprint`: Fingerprint della http ca del cluster elastic. Da settare solo se insecure:false. Da definire nel vault


```