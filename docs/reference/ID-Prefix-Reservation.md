---
title: Prefisso ID prenotazione riferimento
description: Descrizione funzionalità di prenotazione del prefisso ID pacchetto e Guida autore.
author: diverdan92
ms.author: diverdan92
ms.date: 10/09/2017
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 32f83bede42f7643a9a4fed593643eefea0453c1
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981002"
---
# <a name="package-id-prefix-reservation"></a>Prenotazione del prefisso ID pacchetto

I proprietari di pacchetti consente di riservare e proteggere la propria identità riservando i prefissi ID. I consumer di pacchetti vengono forniti con informazioni aggiuntive quando si utilizzano i pacchetti che il pacchetto in uso non sono ingannevole nelle relative proprietà di identificazione. 

[NuGet.org](https://www.nuget.org/) e Visual Studio 2017 versione 15.4 o versioni successive mostrano un indicatore visivo per i pacchetti che vengono inviati dai proprietari con un prefisso dell'ID pacchetto riservato, purché il pacchetto corrisponde l'ID riservato del prefisso modello di denominazione. Il seguente riferimento spiega cosa comporta la prenotazione del prefisso ID e come applicare un proprietario per un prefisso dell'ID.

## <a name="id-prefix-reservation-details"></a>Dettagli della prenotazione prefisso ID

Quando un prefisso dell'ID pacchetto riservato, vengono eseguite diverse operazioni sul [nuget.org](https://www.nuget.org/) raccolta, nonché come in Visual Studio. Inoltre, vengono spostate scenari supportati per le prenotazioni di prefisso ID, ad esempio l'impostazione di un prefisso come 'public', la delega del subset di prefisso a più proprietari.

### <a name="id-prefix-reservation-on-nugetorg"></a>Prenotazione del prefisso ID in nuget.org

Quando un prefisso è riservato in [nuget.org](https://www.nuget.org/), si verificherà quanto segue:

1. Una prenotazione del prefisso è associata un proprietario o un set di proprietari sul [nuget.org](https://www.nuget.org/).

1. Ogni volta che un pacchetto viene inviato a [nuget.org](https://www.nuget.org/) con un ID che corrisponde il prefisso dell'ID riservato, il pacchetto viene rifiutato a meno che non ha origine in proprietari riservato il prefisso dell'ID.

1. I pacchetti che corrisponde al prefisso ID riservato e ha origine dal proprietari riservato il prefisso dell'ID saranno necessario un indicatore visivo in Visual Studio 2017 versione 15.4 o versioni successive e nel [nuget.org](https://www.nuget.org/) che indica che il pacchetto si trova sotto prefisso ID riservato. Questo vale per gli invii di nuovo pacchetto oltre a pacchetti esistenti in proprietari. **Nota:** l'indicatore in Visual Studio viene visualizzato solo se si seleziona un singolo feed come origine del pacchetto.

1. Tutti i pacchetti già esistenti che corrispondono al prefisso ID riservato, ma che sono *non* appartenenti al proprietario di riservato prefisso rimarrà invariato (non potranno essere rimossi dall'elenco, ma non avranno anche l'indicatore visivo). Inoltre, i proprietari di questi pacchetti ancora potranno inviare nuove versioni per il pacchetto.

Queste modifiche si basano sulle condizioni seguenti e impongano restrizioni aggiuntive diversi:

- Solo un proprietario di un pacchetto deve avere il prefisso riservato per l'indicatore visivo da visualizzare (per i pacchetti con più proprietari).

- Se è presente più di un proprietario di un pacchetto in cui uno o più proprietari ha il prefisso riservato e uno o più proprietari non è il prefisso riservato, solo i proprietari indicati con il prefisso riservato possono rimuovere altri proprietari con un prefisso riservato. I proprietari che non hanno il prefisso riservato non è possibile rimuovere proprietari con il prefisso riservato. Possono comunque rimuovere altri proprietari che inoltre non è il prefisso riservato.

- Una volta che un pacchetto include l'indicatore visivo, dovrebbe *sempre* hanno l'indicatore visivo (garantendo che almeno un proprietario con il prefisso riservato rimarrà sempre un proprietario)

### <a name="advanced-prefix-reservation-scenarios"></a>Scenari di prenotazione prefisso avanzate

Esistono diversi scenari prenotazione prefisso più avanzati descritti di seguito, tra cui la delega subprefix e i prefissi di contrassegno come pubblico. Di seguito sono le prenotazioni di prefisso più avanzate che possono essere apportate. 

- Durante la prenotazione del prefisso, il proprietario può richiedere la delega di subset di prefisso (o il prefisso) di altri proprietari. Ad esempio, se '[Microsoft](https://www.nuget.org/profiles/microsoft)' proprietario ' Microsoft.\*', ma '[aspnet](https://www.nuget.org/profiles/aspnet)' vuole riservare ' Microsoft.AspNet.\*','[Microsoft](https://www.nuget.org/profiles/microsoft)' can scegliere di delegare ' Microsoft.AspNet. \*' per il [aspnet](https://www.nuget.org/profiles/aspnet) account.

- Durante la prenotazione del prefisso, il proprietario può scegliere di rendere pubblico un prefisso. Si continuerà a fornire loro l'indicatore visivo che mostra che il pacchetto proviene da un prefisso riservato, ma potrà **non** invii pacchetto future sul prefisso per qualsiasi proprietario di blocco. Ciò è utile per progetti open source con tanti collaboratori: i collaboratori top o core possono avere il prefisso riservato, ma può comunque essere aperta per tutti i collaboratori. 

### <a name="prefix-reservation-visual-indicator"></a>Indicatore visivo di prenotazione del prefisso

Quando un pacchetto proviene da un prefisso riservato, viene visualizzato il sotto gli indicatori visivi sul [nuget.org](https://www.nuget.org/) gallery e in Visual Studio 2017 versione 15.4 o versioni successive:

**Raccolta NuGet.org**
![raccolta nuget.org](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Processo dell'applicazione di prenotazione prefisso ID

1. Esaminare l'accettazione [criteri per la prenotazione del prefisso ID](#id-prefix-reservation-criteria).

2. Determinare i prefissi da impostare come riservati, oltre a eventuali [prefisso prenotazione scenari avanzati](#advanced-prefix-reservation-scenarios) potrebbe essere necessaria.

3. Inviare un messaggio a [ account@nuget.org ](mailto:account@nuget.org) con il proprietario del nome visualizzato sul [nuget.org](https://www.nuget.org/), oltre a qualsiasi prefisso riservato richiesta. Subset di prefisso consentono di delegare a più proprietari, assicurarsi che si citare tutti i nomi visualizzati di proprietario e subset del prefisso.

Dopo l'applicazione è stata inviata, ricevono una notifica di accettazione o rifiuto (con i criteri che ha causato il rifiuto). Si potrebbe essere necessario porre le domande di identificazione aggiuntive per verificare l'identità del proprietario.

### <a name="id-prefix-reservation-criteria"></a>Criterio di prenotazione di prefisso ID

Durante la revisione di tutte le applicazioni per la prenotazione del prefisso ID, il [nuget.org](https://www.nuget.org/) team valuterà l'applicazione con i seguenti criteri. Non tutti i criteri deve essere soddisfatta per un prefisso a essere riservato, ma l'applicazione potrebbe essere negata se non sono sostanziali per constatare i criteri rispettati (con una spiegazione di base):

1. Il prefisso dell'ID pacchetto corretto e chiarezza identifica il proprietario del pacchetto?

1. Sono un numero significativo di pacchetti che sono già stati inviati dal proprietario del sotto il prefisso dell'ID pacchetto?

1. Il prefisso dell'ID pacchetto è un elemento comune che non devono appartenere a qualsiasi singolo proprietario o organizzazione?

1. Verrebbe *non* riservare il prefisso dell'ID pacchetto causare ambiguità e confusione per gli altri utenti?

1. Sono le proprietà di identificazione dei pacchetti che soddisfano il prefisso ID pacchetto chiaro e coerente (in particolare l'autore del pacchetto)?

## <a name="third-party-feed-provider-scenarios"></a>Scenari di provider di feed di terze parti

Se un provider di feed di terze parti è interessato a implementare i propri servizi per fornire le prenotazioni di prefisso, è possibile farlo modificando il servizio di ricerca in NuGet V3 feed provider. L'aggiunta del servizio di ricerca di feed consiste nell'aggiungere il *verificato* , proprietà ed esempi per i feed V3 riportato di seguito. Il client di NuGet non supporta l'aggiunta della proprietà nella versione 2 del feed.

Per altre informazioni, vedere la [documentazione sul servizio di ricerca dell'API](../api/search-query-service-resource.md).

## <a name="package-id-prefix-reservation-dispute-policy"></a>Pacchetto prefisso ID prenotazione delle controversie sui criteri
Se si ritiene che un proprietario nella [NuGet.org](https://www.nuget.org) è stata assegnata una prenotazione del prefisso ID pacchetto supera i criteri elencati sopra, o gli utenti su qualsiasi marchi o copyright,. messaggio di posta elettronica [ support@nuget.org ](mailto:support@nuget.org)con il prefisso dell'ID in questione, il proprietario del prefisso ID e il motivo per contesta la prenotazione del prefisso assegnato.

