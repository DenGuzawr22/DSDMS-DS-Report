---
title: Usage Examples
has_children: false
nav_order: 9
---

# Esempi di utilizzo

Il progetto sviluppato, si è posto l'obiettivo di sviluppare un sistema basato su Microservizi, che andasse a supportare ed eventualmente migliorare le funzionalità fornite da una Scuola Guida.
L'obiettivo è stato quindi il solo sviluppo del back-end ti tale applicativo, in modo da fornire tutte le API necessarie allo sviluppo di un applicativo di front-end correlato.

In particolare, gli ambiti che sono stati tenuti in considerazione, successivamente ad alcuni colloqui con il committente sono i seguenti:
- Gestione degli esami pratici e teorici, relative prenotazioni e registrazione dei risultati, visita con il dottore;
- Gestione dei documenti di ciascun Iscritto: foglio rosa, conteggio guide, conteggio esami teorici;
- Gestione dei veicoli e delle guide pratiche;
- Gestione degli iscritti e delle relative informazioni personali.

Di seguito viene riportato un esempio di utilizzo delle API messe a disposizione, per il successivo sviluppo di un'interfaccia grafica.

## Registrazione di una guida pratica

Innanzitutto è necessario connettersi al microservizio *Driving Service*, istanziato sulla porta 8010 di localhost.
Per la connessione viene utilizzato WebClient, relativo alla libreria Vertx, utilizzata all'interno del progetto.

```Kotlin        
val options: WebClientOptions = WebClientOptions()
    .setDefaultPort(8010)
    .setDefaultHost("driving_host")

return WebClient.create(Vertx.vertx(), options)
```

Avendo eseguito la connessione, possiamo procedere con l'utilizzo delle API messe a disposizione dal microservizio voluto, visualizzabili mediante [Documentazione OpenAPI](https://app.swaggerhub.com/apis/DenGuzawr22/DSDMS/latest) .

L'obiettivo dell'esempio riportato è quello di registrare una guida pratica su strada, svolto come mostrato.

```Kotlin
val request = client
    .post("/drivingSlots")
    .sendBuffer(
        Buffer.buffer(
            Json.encodeToString(
                DrivingSlotBooking(
                    LocalDate.parse(date),
                    LocalTime.parse(time),
                    instructorId,
                    dossierId,
                    DrivingSlotType.ORDINARY,
                    LicensePlate(vehicle),
                ),
            )
        ),
    )
```

L'invio delle informazioni avviene sempre mediante formati standard e riconoscibili visualizzati mediante schemi Json. Conseguentemente viene utilizzato un Buffer per effettuare l'encoding del modello Json necessario. Per ciascuna chiamata di tipo Post o Put, i rispettivi schemi Json, sono visibile all'interno di ciascun microservizio o nella documentazione OpenAPI.

Infine riceveremo una risposta positiva o negativa dal rispettivo microservizio, gestibile e visualizzabile mediante i seguenti comandi.
Le tipologie di conferma o di errore ricevibili, sono anch'esse mostrate nella relativa documentazione OpenAPI, al link precedentemente inserito.

```Kotlin
val response = waitResult(request)

statusMessage = response.body().toString()
statusCode = response.statusCode()
```

## Registrazione di un nuovo Dossier

Di seguito viene mostrata la procedura per la registrazione di un nuovo Dossier nel sistena.

Apertura della connessione al microservizio *Dossier Service*, istanziato sulla porta 8000 di Localhost.

```Kotlin        
val options: WebClientOptions = WebClientOptions()
    .setDefaultPort(8000)
    .setDefaultHost("dossier_host")

return WebClient.create(Vertx.vertx(), options)
```

Come nell'esempio precedente, visualizzando la documentazione OpenAPI, procediamo con la chiamata alla rotta messa a disposizione per l'operazione simulata.

```Kotlin
val request = client
    .post("/dossiers")
    .sendBuffer(
        Buffer.buffer(
            Json.encodeToString(
                SubscriberDocuments(name, surname, LocalDate.parse(birthdate), fiscal_code)
            )
        )
    )
```

Attendiamo una rispsota dal server e gestiamo/visualizziamo il contenuto.
Anche in questo caso, dalla documentazione OpenAPI è possibile esaminare le risposte ottnibili da parte del server.

```Kotlin
val response = waitResult(request)

statusMessage = response.body().toString()
statusCode = response.statusCode()
```