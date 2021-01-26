---
title: Governance dei progetti per NuGet
description: Modello di governance per NuGet, inclusi ruoli e responsabilità per committer, collaboratori e utenti.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 2edaac0218dc936ea6bfe1814c0aab963028ea87
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775594"
---
# <a name="nuget-governance"></a>Governance per NuGet

> Questo documento si basa sul [modello di governance con dittatore benevolo](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) dell'Università di Oxford. È concesso in licenza con una [Licenza Attribuzione - Condividi allo stesso modo 2.0 Regno Unito: Inghilterra e Galles di Creative Commons](http://creativecommons.org/licenses/by-sa/2.0/uk/).

Il progetto NuGet è condotto da in dittatore benevolo e gestito dalla community. Questo significa che la community contribuisce attivamente alla manutenzione quotidiana del progetto, ma la linea strategica generale è stabilita dal dittatore benevolo. In caso di disaccordo, l'ultima parola spetta al dittatore benevolo.

È responsabilità del dittatore benevolo risolvere eventuali controversie all'interno della community e garantire che il progetto possa evolversi in modo coordinato. È invece responsabilità della community guidare le decisioni del dittatore benevolo tramite partecipazione e contributi attivi.

## <a name="roles-and-responsibilities"></a>Ruoli e responsabilità

Sono quattro i ruoli descritti in questo articolo, ovvero dittatore benevolo, committer, collaboratori e utenti.

### <a name="benevolent-dictator"></a>Dittatore benevolo

Il team principale di NuGet si è autonominato dittatore benevolo o responsabile del progetto. Tuttavia, dato che la community ha sempre la possibilità di creare copie tramite fork, il team è tenuto a rispondere in toto alla community. Il responsabile del progetto è tenuto a comprendere la community nel suo complesso e a cercare di soddisfare il maggior numero di esigenze in conflitto possibile, assicurando allo stesso tempo la sopravvivenza del progetto a lungo termine.

Da molti punti di vista, il ruolo di dittatore benevolo ha poco a che fare con la dittatura e molto di più con la diplomazia. La chiave è garantire che, man mano che il progetto si espande, le persone giuste abbiano influenza sul progetto e che la community condivida ampiamente la visione del responsabile del progetto. Il responsabile è tenuto ad assicurare che i committer (vedere di seguito) prendano le giuste decisioni per il buon esito del progetto. In generale, fino a quando i committer operano in linea con la strategia del progetto, il responsabile del progetto consentirà loro di procedere nel modo desiderato.

Inoltre, il personale di .NET Foundation considera il responsabile del progetto il contatto principale o prioritario per NuGet ai fini di operazioni commerciali come le registrazioni dei servizi e per i servizi tecnici, come la firma del codice.

### <a name="committers"></a>Committer

I committer sono collaboratori che contribuiscono in modo significativo e continuativo al progetto NuGet e vengono designati dal dittatore benevolo. Dopo la nomina, i committer hanno la responsabilità sia di scrivere codice direttamente nel repository, sia di filtrare i contributi di altri utenti. I committer sono spesso sviluppatori, ma possono contribuire in altri modi.

In genere, un committer si concentra su un aspetto specifico del progetto e offre un livello di esperienza e conoscenze che gli accorda il rispetto della community e del responsabile del progetto. Il ruolo di committer non è ufficiale, è semplicemente una posizione assunta dai membri esperti della community, quando il responsabile del progetto si rivolge a loro per richiedere indicazioni e supporto.

I committer non esercitano alcuna autorità in merito alla direzione generale del progetto NuGet. Sono tuttavia ascoltati dal responsabile del progetto. Il committer è tenuto ad assicurarsi che il responsabile sia a conoscenza delle esigenze e degli obiettivi collettivi della community e a contribuire allo sviluppo o alla sollecitazione di contributi appropriati per il progetto. Ai committer viene spesso accordato il controllo informale delle loro aree di responsabilità specifiche e vengono loro assegnati i diritti per la modifica diretta di determinate aree del codice sorgente. Ciò significa che, anche se i committer non hanno un'autorità decisionale esplicita, spesso si ritroveranno a compiere azioni in linea con le decisioni prese dal responsabile.

### <a name="contributors"></a>Autori di contributi

I collaboratori sono membri della community che inviano patch per NuGet. Queste patch possono essere singoli contributi oppure periodiche. Ci si aspetta che i collaboratori inviino patch inizialmente piccole e progressivamente più estese, man mano che il collaboratore, i committer e il responsabile del progetto acquisiscono sicurezza sulla qualità delle patch di un collaboratore. Per i collaboratori è previsto un riconoscimento nel documento delle note sulla versione del prodotto associato.

Prima che la prima patch di un collaboratore venga inserita nel repository, il collaboratore deve firmare un [contratto di licenza per i collaboratori](http://en.wikipedia.org/wiki/Contributor_License_Agreement) o un contratto di assegnazione per .NET Foundation. La patch può essere inviata e discussa, ma non ne verrà eseguito il commit nel repository se i documenti appropriati non sono pronti. Per ottenere un contratto di licenza con collaboratore, inviare una richiesta tramite posta elettronica a [contributions@nuget.org](mailto:contributions@nuget.org) .

Per diventare un collaboratore, inviare una richiesta di pull a uno dei repository seguenti:

- [Client NuGet](https://github.com/NuGet/NuGet.Client)
- [Raccolta NuGet](https://github.com/nuget/nugetgallery)
- [Documentazione NuGet](https://github.com/nuget/nugetdocs)

Il processo dettagliato per l'invio di una richiesta pull varia in base al repository:

- [Contribution instructions for NuGet Client and NuGet Gallery (Istruzioni per l'invio di contributi per il client NuGet e la raccolta NuGet)](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [Contribution instructions for NuGet Docs (Istruzioni per l'invio di contributi per la documentazione NuGet)](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a>Utenti

Gli utenti sono membri della community a cui serve NuGet e che lo usano, come i consumer di pacchetti e/o gli autori. Gli utenti sono i membri più importanti della community: senza di loro il progetto non avrebbe alcuno scopo. Chiunque può essere un utente, non sono previsti requisiti specifici.

Gli utenti devono essere incoraggiati a partecipare il più possibile alla vita del progetto NuGet e alla community. I contributi degli utenti consentono al team del progetto di assicurarsi che vengano soddisfatte le esigenze di tali utenti. Le attività comuni degli utenti includono a titolo di esempio le seguenti:

- Promuovere l'uso del progetto
- Informare gli sviluppatori dei punti di forza e di debolezza del progetto dal punto di vista di un nuovo utente
- Offrire supporto morale (i ringraziamenti sono sempre molto utili)
- Scrivere documentazione ed esercitazioni
- Creare report di bug e richieste di funzionalità
- Partecipare agli eventi della community, come i bug bash
- Partecipare ad aree discussioni o forum

Gli utenti che continuano a partecipare al progetto e alla community, spesso si ritroveranno a essere sempre più coinvolti. Tali utenti potrebbero quindi diventare collaboratori, come descritto in precedenza.

## <a name="package-succession-under-special-circumstances"></a>Successione per i pacchetti in circostanze speciali

Nei casi sfortunati di incapacità o decesso del titolare di un account NuGet, si collaborerà con la community per assegnare uno o più titolari appropriati al pacchetto, nel caso l'account sia di proprietà esclusiva e il pacchetto sia pubblicato con una [licenza approvata da OSI](https://opensource.org/licenses/alphabetical). Per richiedere la proprietà è necessario inviare i documenti seguenti:

1. Fotocopia della carta di identità.
1. Uno dei documenti seguenti comprovanti lo stato del titolare dell'account precedente: 
    - Un certificato di morte ufficiale in caso di decesso del titolare dell'account precedente, o,
    - Un documento certificato, ad esempio un certificato firmato dal medico professionista che ha in cura il titolare dell'account risultato incapace.
1. Uno dei documenti seguenti comprovanti il diritto di proprietà: 
    - Certificato di matrimonio che dimostra che l'utente richiedente è il coniuge superstite del titolare dell'account,
    - Procura firmata,
    - Copia del testamento o di un accordo fiduciario da cui l'utente richiedente risulta esecutore o beneficiario,
    - Certificato di nascita del titolare dell'account, nel caso l'utente richiedente sia un genitore, o,
    - Documentazione della tutela, nel caso l'utente richiedente sia un tutore legale del titolare dell'account.

Se si ritiene di dover richiamare questi criteri, inviare un messaggio di posta elettronica all'indirizzo [support@nuget.org](mailto:support@nuget.org) con l'ID e la versione del pacchetto.

## <a name="transparency"></a>Trasparenza

Per la riuscita di un progetto open source è fondamentale che la community possa avere fiducia nella governance. A tale scopo, il processo decisionale deve essere trasparente e aperto. Le discussioni sulla direzione del progetto deve essere condotte pubblicamente. La community non deve mai essere colta di sorpresa da una decisione del dittatore benevolo. Le discussioni sulle decisioni per il progetto devono inoltre essere archiviate in modo che i membri della community possano comprendere l'intero iter di una decisione e il relativo contesto.
