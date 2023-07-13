---
title: Deployment
has_children: true
nav_order: 8
---

# Deployment

Questa sezione, vuole analizzare nel dettaglio le procedure utilizzate nel progetto per il deployment del sistema a microservizi, sviluppato.

In particolare si è deciso di seguire tecniche DevOps per la build automation e le automatic release, insieme all'utilizzo di Gradle come tool principale.
Il tutto risulta virtualizzato mediante container docker, che ne consentono e facilitano l'esecuzione su diversi ambienti.

### Struttura multi-progetto
Il progetto è stato sviluppato come un gradle multi progetto composto da cinque sotto-progetti. Quattro di questi sono dedicati a ciascun bounded context individuato, mentre un ultimo denominato *SystemTester* è stato creato per simulare un client e testare l'intero sistema di microservizi. 
Questo approccio presenta diversi vantaggi:
- Innanzitutto, consente di ottenere una struttura modulare e separata, fondamentale per lo sviluppo dei microservizi;
- Ogni bounded context viene gestito in modo indipendente, consentendo agli sviluppatori di concentrarsi sulle funzionalità specifiche di ciascun microservizio.

Inoltre, grazie all'approccio multi-project, è possibile condividere il codice di configurazione di Gradle tra i vari sotto-progetti e importare alcune classi su "SystemTester", semplificando il processo di testing. Questa condivisione del codice di configurazione aiuta a ridurre la duplicazione e a mantenere una coerenza nelle impostazioni di build e dipendenze.

### Task personalizzati
Per ogni sotto-progetto sono stati creati dei task personalizzati e sono stati inseriti all’interno dei relativi file `build.gradle.kts`.

In particolare per ciascuno sono stati configurati o creati vari task, tra cui:
- `ShadowJar` che permette la generazione di un jar eseguibile. La configurazione:
  - Specifica la Main class;
  - Assegna un nome personalizzato che può includere la versione del sistema;
  - Specifica la cartella di destinazione.
- `createJavadoc` permette la generazione degli artefatti assieme alla documentazione Javadoc.
