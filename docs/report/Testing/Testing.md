---
title: Testing
has_children: true
nav_order: 7
---

# Testing

Per verificare il corretto funzionamento del sistema e l'efficienza dei servizi forniti al cliente,
si è proceduto a testare le diverse componenti del sistema, mediante Acceptance Testing Driven Development.
Il testing avviene su due fronti:
- test locali, all'interno di ciascun microservice;
- black-box test (a scatola chiusa), che rappresentano una porzione per la verifica del progetto.
  
Nelle successive sezioni verranno descritti in maggiore dettaglio i test realizzati e le motivazioni che vanno a supportare le scelte implementative effettuate.

Non verranno invece riportate, verifiche sul coverage del progetto fornito, in quanto solo una piccola porzione del codice dei microservice viene testata mediante test locali. Un client "dummy", viene utilizzato per eseguire acceptance test "a scatola chiusa", forniti al committente, verificando il soddisfacimento dei requisiti funzionali e non funzionali imposti.