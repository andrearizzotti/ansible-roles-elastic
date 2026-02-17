# ansible-roles-elastic

Playbook dedicato all'installazione dell'elastic agent su tutti gli host compatibili.

Il playbook richiama 3 ruoli:

* `install_agent_linux`: installa l'agente su host con os Linux (Debian e RedHat)
* `install_fleet_server`: installa l'agente su host con os Linux (Debian e RedHat)
* `install_agent_windows`: installa l'agente su host con os Windows
* `install-kibana-9x-Redhat`: installa e configura kibana versione 9.x su macchine redhat


Gli host windows e linux devono essere gestiti nell'inventory con appositi gruppi.

## install_agent_linux e install_agent_windows

Per i ruoli install_agent_linux e install_agent_windows è necessario configurare le seguenti variabili:

* `elastic_agent_version`: versione dell'agente da installare (deve essere la stessa di elasticsearch)
* `fleet_server_url`: url per connettersi al fleet server (componente elastic per la gestione centralizzata degli agent)
* `enrollment_token`: token da utilizzare per connettersi al fleet server. Da definire nel vault
* `install_dir`: directory di installazione. Facoltativa in quanto già settata di default all'interno del ruolo

## install_fleet_server

Per l'installazione del fleet server sono da configurare le seguenti variabili:

* `elastic_agent_version`: versione dell'agente da installare (deve essere la stessa di elasticsearch)
* `elastic_url`: url per connettersi a elasticsearch 
* `fleet_server_service_token`: token da utilizzare per l'installazione del fleet server. Da definire nel vault
* `install_dir`: directory di installazione. Facoltativa in quanto già settata di default all'interno del ruolo
* `fleet_server_policy`: Policy da utilizzare per l'installazione del fleet server. Facoltativa in quanto già settata di default all'interno del ruolo
* `fleet_server_port`: Porta in ascolto sul fleet server. Facoltativa in quanto già settata di default all'interno del ruolo
* `insecure`: booleano, definisce se utilizzare la modalita' insecure (comunicazione con elasticsearch senza verifica del certificato). Facoltativa in quanto già settata di default a False all'interno del ruolo
* `fleet_server_es_ca_trusted_fingerprint`: Fingerprint della http ca del cluster elastic. Da settare solo se insecure:false. Da definire nel vault

## install-kibana-9x-Redhat

Il ruolo è stato pensato e testato per l'installazione di kibana alla versione 9.x. Questo non esclude che il ruolo possa essere usato per installazioni minimali di versioni precedenti o successive.
Per l'installazione e configurazione di kibaba sono da configurare le seguenti variabili:

* `es_major_version`: major version da installare, di default è 9.x
* `es_version`: versione da installare, di default è 9.3.0 
* `kibana_port`: porta del servizio kibana. Di default è 5601
* `kibana_es_security_enabled`: Definisce se utilizzare o meno il protocollo https con elastcsearch. Default a false
* `audit_logging_enabled`: Definisce se abilitare o meno gli audit log. Default a false
* `kibana_server_publicBaseUrl`: Impostazione server.publicBaseUrl, definisce l'endpoint su sui raggiungere kibana da browser. Facoltativo
* `elasticsearch_hosts`: Lista di server elasticsearch a cui connettersi. Esempio:

```yaml
elasticsearch_hosts:
  - https://10.30.129.54:9200
  - https://10.30.128.109:9200
  - https://10.30.129.47:9200
```

* `xpack_encryptedSavedObjects_encryptionKey`: Chiave di cifratura interna di kibana. Da impostare nel vault
* `xpack_reporting_encryptionKey`: Chiave di cifratura interna di kibana. Da impostare nel vault
* `xpack_security_encryptionKey`: Chiave di cifratura interna di kibana. Da impostare nel vault
* `elasticsearch_username`: Nome dell'utenza da usare per la comunicazione con elasticsearch. Suggerito kibana_system
* `elasticsearch_password`: Password dell'utenza. Da impostare nel vault
