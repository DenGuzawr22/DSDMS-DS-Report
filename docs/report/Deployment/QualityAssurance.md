---
title: Quality Assurance
has_children: false
parent: Deployment
nav_order: 8
---

# Quality Assurance
Per garantire la qualità del codice e dello sviluppo, sono stati utilizzati i seguenti Gradle Plugin:
- **Gradle pre-commit Git Hooks**: Questo plugin crea un Git Hook che impedisce di effettuare un commit se non viene rispettato il formato [Conventional commits](https://www.conventionalcommits.org/en/v1.0.0/). I "Conventional Commits" sono una convenzione per scrivere messaggi di commit strutturati in un formato specifico, che facilita l'automazione delle versioni e la generazione delle note di release. 
- **Ktlint**: Questo plugin permette di mantenere uno stile uniforme nel codice Kotlin. Ktlint applica regole di formattazione del codice predefinite o personalizzate all'interno del progetto. Assicurarsi che tutto il codice Kotlin sia formattato in modo coerente facilita la leggibilità del codice e promuove buone pratiche di sviluppo.
- **Detect**: Questo plugin consente di eseguire un'analisi statica del codice per identificare e prevenire diversi tipi di potenziali problemi. Ad esempio, il plugin può individuare vulnerabilità nella sicurezza del codice, dipendenze non conformi, violazioni delle best practice di sviluppo e altre problematiche simili.