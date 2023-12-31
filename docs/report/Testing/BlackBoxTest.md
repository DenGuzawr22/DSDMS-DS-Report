---
title: BlackBox Test
has_children: false
parent: Testing
nav_order: 7
---

## Black-Box Test
Come anticipato, questa tipologia di test nasce dalla necessità di verificare le API messe a disposizione dai singoli microservice
a "scatola-chiusa", senza quindi tener conto delle logiche interne.
Per eseguire questi test, si è deciso d'implementare un client "dummy": System Tester, sul quale
come framework di Testing viene adottato Cucumber.

### System Tester
System Tester rappresenta un client "dummy", inserito nel progetto per verificare il funzionamento
delle API dei singoli microservice, a "Scatola chiusa".
Ciascuna API e ciascun microservice viene testata con l'utilizzo del framework Cucumber, mediante scenari e step espressi in un linguaggio facilmente comprensibile anche per l'utente finale.
Questo consente di verificare il soddisfacimento dei requisiti imposti dal committente del software, verificando
ciascuna risposta ottenuta successivamente a ogni interrogazione.

Per ciascuna risposta, si verificano alcuni parametri fondamentali:
- status code: rappresenta il codice HTTP che viene restituito (codice 200 per OK, codice 400 per BAD REQUEST sono spesso utilizzati);
- body: contiene un payload ottenuto dalla richiesta (un Dossier, un Driving Slot) o un messaggio di errore/di conferma.

### Cucumber
Cucumber è un framework che consente l'implementazione di Acceptance Testing. Viene utilizzato per la scrittura di test funzionali, utilizzando Gherkin, come linguaggio per la definizione degli scenari con linguaggio naturale e ben comprensibile, anche dal committente.
L'utilizzo di questa metodologia di test, ha anche consentito di creare una connessione tra il team di sviluppo e l'utente, che riesce a comprendere con facilità lo scopo e il funzionamento dei test di accettazione forniti, potendolo inserire efficacemente nel processo di sviluppo.

I test di accettazione, eseguiti mediante cucumber, consentono di verificare il soddisfacimento di requisiti funzionali e non funzionali, specificati dal cliente o dagli utenti finali. Essi rappresentano infatti, l'ultima fase del ciclo di vita del software, eseguiti solo successivamente ai test locali precedentemente descritti.

Di seguito un esempio dell'utilizzo di Cucumber e del linguaggio Gherkin per l'esecuzione di Acceptance Testing.
In particolare viene verificata l'API per la registrazione di un Iscritto su DossierService, con differenti set d'informazioni, senza tener conto del codice "di basso livello", ma solamente verificando le risposte ottenute.

Nel primo scenario, vengono fornite informazioni corrette, la creazione viene correttamente eseguita, restituendo l'Id del dossier creato.
Verificando l'Id fornito, otteniamo nel Body il Dossier completo in formato Json, dal quale possiamo visualizziamo che exam status è stato correttamente inizializzato.
Nel secondo scenario, forniamo a DossierService dei dati invalidi, viene quindi restituito per ogni set di valori, una differente tipologia di errore.

```
Feature: Registration subscriber documents and reading dossier information
  Scenario Outline: subscriber information's are correct
    When I register subscriber's documents information: <name>,<surname>,<birthdate>,<fiscal_code>
    Then I received an id of registered dossier
    When I search dossier by received id
    Then I find <name>,<surname>,<birthdate>,<fiscal_code> of registered dossier
    And It has not done both practical and theoretical exams

    Examples: basic information
        | name | surname | birthdate | fiscal_code |
        | Riccardo | Bacca | 1999-03-07 | BCCRCR99C07C573X |

    Scenario Outline: The subscriber documents information has invalid values
        When I try to register invalid subscriber information: <name>,<surname>,<birthdate>,<fiscal_code>
        Then I get <error_type> error type

    Examples: invalid subscriber information
        | name | surname | birthdate | fiscal_code | error_type |
        | Riccardo | Bacca | 1999-03-07 | BCCRCR99C07C573X | VALID_DOSSIER_ALREADY_EXISTS |
        | Ricca    | Bacca | 2015-03-07 | BCCRCR99C07C573K | AGE_NOT_SUFFICIENT           |
        | b        | 123   | 1999-03-07 | BCCRCR99C07C573L | NAME_SURNAME_NOT_STRING      |
```