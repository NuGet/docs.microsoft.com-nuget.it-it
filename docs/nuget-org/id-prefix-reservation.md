---
title: Prenotazione del prefisso ID
description: Descrizione della funzionalità di prenotazione del prefisso ID del pacchetto e guida alla creazione.
author: karann-msft
ms.author: karann
ms.date: 09/07/2019
ms.topic: reference
ms.reviewer: karann
ms.openlocfilehash: f6c4a18366b4df20fb210f718d3779e85c08d550
ms.sourcegitcommit: 188ade66b7ac807ba1667c77cfb9325bf89a8a4a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/24/2019
ms.locfileid: "71248131"
---
# <a name="package-id-prefix-reservation"></a>Prenotazione del prefisso ID del pacchetto

I proprietari di pacchetti possono prenotare e proteggere la propria identità prenotando i prefissi ID. Per i consumer di pacchetti vengono fornite informazioni aggiuntive quando i pacchetti che utilizzano non sono ingannevoli nelle proprietà di identificazione. 

[nuget.org](https://www.nuget.org/) e Visual Studio 2017 versione 15.4 o successive hanno un indicatore visivo per i pacchetti inviati dai proprietari con un prefisso ID di pacchetto riservato, purché il pacchetto corrisponda al criterio di denominazione del prefisso ID riservato. Il seguente riferimento spiega cosa comporta la prenotazione del prefisso ID e come un proprietario può richiedere un prefisso ID.

## <a name="id-prefix-reservation-details"></a>Dettagli della prenotazione del prefisso ID

Quando si prenota un prefisso ID del pacchetto, vengono eseguite diverse operazioni nella raccolta [nuget.org](https://www.nuget.org/), nonché in Visual Studio. Inoltre, le prenotazioni dei prefissi ID supportano scenari avanzati, ad esempio l'impostazione di un prefisso come "pubblico", con la delega di subset di prefissi a più proprietari.

### <a name="id-prefix-reservation-on-nugetorg"></a>Prenotazione del prefisso ID in nuget.org

Quando un prefisso viene prenotato in [nuget.org](https://www.nuget.org/), si verifica quanto segue:

1. Una prenotazione del prefisso è associata un proprietario o un gruppo di proprietari in [nuget.org](https://www.nuget.org/).

1. Ogni volta che un pacchetto viene inviato a [nuget.org](https://www.nuget.org/) con un ID che corrisponde al prefisso ID riservato, il pacchetto viene rifiutato a meno che non abbia origine da proprietari che hanno prenotato il prefisso ID.

1. I pacchetti che corrispondono al prefisso ID riservato e hanno origine da proprietari che hanno prenotato il prefisso ID avranno un indicatore visivo in Visual Studio 2017 versione 15.4 o successive e in [nuget.org](https://www.nuget.org/) per indicare che il pacchetto fa riferimento a un prefisso ID riservato. Questo vale sia per gli invii di nuovi pacchetti, sia per i pacchetti già esistenti dei proprietari. **Nota:** L'indicatore in Visual Studio viene visualizzato solo se si seleziona un singolo feed come origine del pacchetto.

1. Tutti i pacchetti già esistenti che corrispondono al prefisso ID riservato, ma *non* appartengono al proprietario del prefisso riservato rimangono invariati ovvero non verranno rimossi dall'elenco, ma non avranno l'indicatore visivo. Inoltre, i proprietari di questi pacchetti saranno comunque in grado di inviare nuove versioni al pacchetto.

Queste modifiche si basano sulle condizioni seguenti e impongono diverse altre restrizioni:

- Solo un proprietario di un pacchetto deve avere il prefisso riservato perché sia visualizzato l'indicatore visivo (per i pacchetti con più proprietari).

- Se esiste più di un proprietario per un pacchetto per cui uno o più proprietari hanno il prefisso riservato e uno o più proprietari non lo hanno, solo i proprietari con prefisso riservato possono rimuovere altri proprietari con prefisso riservato. I proprietari che non hanno il prefisso riservato non possono rimuovere i proprietari con il prefisso riservato. Possono comunque rimuovere altri proprietari che non hanno il prefisso riservato.

- Se un pacchetto include l'indicatore visivo, deve *sempre* avere l'indicatore visivo (garantendo che almeno un proprietario con prefisso riservato rimanga sempre un proprietario)

### <a name="advanced-prefix-reservation-scenarios"></a>Scenari di prenotazione avanzata del prefisso

Esistono numerosi altri scenari di prenotazione più avanzata del prefisso, tra cui la delega di prefissi secondari e il contrassegno dei prefissi come pubblici. Di seguito sono riportate le prenotazioni di prefisso più avanzate che è possibile effettuare. 

- Durante la prenotazione del prefisso, il proprietario può richiedere la delega di subset di prefissi (o del prefisso) ad altri proprietari. Ad esempio, se '[Microsoft](https://www.nuget.org/profiles/microsoft) è proprietario di Microsoft.\*, ma [aspnet](https://www.nuget.org/profiles/aspnet) vuole prenotare Microsoft.AspNet.\*, [Microsoft](https://www.nuget.org/profiles/microsoft) può scegliere di delegare Microsoft.AspNet.\* all'account [aspnet](https://www.nuget.org/profiles/aspnet).

- Durante la prenotazione del prefisso, il proprietario può scegliere di rendere pubblico un prefisso. In questo modo continuerà a essere disponibile l'indicatore visivo che indica che il pacchetto proviene da un prefisso riservato, ma **non** verranno bloccati i futuri invii di pacchetti al prefisso per qualsiasi proprietario. Ciò è utile per progetti open source a cui contribuiscono molti utenti: i collaboratori più importanti possono avere il prefisso riservato, ma il progetto rimane aperto a tutti i collaboratori. 

### <a name="prefix-reservation-visual-indicator"></a>Indicatore visivo della prenotazione del prefisso

Quando un pacchetto proviene da un prefisso riservato, nella raccolta [nuget.org](https://www.nuget.org/) e in Visual Studio 2017 versione 15.4 o successive vengono visualizzati i seguenti indicatori visivi:

**Raccolta nuget.org**
![Raccolta nuget.org](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Processo di applicazione della prenotazione del prefisso ID

1. Esaminare i [criteri di accettazione per la prenotazione del prefisso ID](#id-prefix-reservation-criteria).

2. Determinare i prefissi che si vuole prenotare, oltre a eventuali [scenari di prenotazione avanzata del prefisso](#advanced-prefix-reservation-scenarios) che potrebbero essere necessari.

3. Inviare un messaggio a [account@nuget.org](mailto:account@nuget.org) con il nome del proprietario visualizzato in [nuget.org](https://www.nuget.org/), oltre a eventuali prefissi riservati che si vuole richiedere. Se si delegano subset di prefissi a più proprietari, assicurarsi di indicare tutti i nomi visualizzati dei proprietari e i subset di prefissi.

Dopo l'invio dell'applicazione si riceve una notifica di accettazione o rifiuto (con i criteri che hanno causato il rifiuto). Potrebbe essere necessario porre altre domande di identificazione per verificare l'identità del proprietario.

### <a name="id-prefix-reservation-criteria"></a>Criteri di prenotazione del prefisso ID

Durante la revisione di un'applicazione per la prenotazione del prefisso ID, il team di [nuget.org](https://www.nuget.org/) valuta l'applicazione rispetto ai criteri indicati di seguito. Non è necessario che siano soddisfatti tutti i criteri perché un prefisso venga riservato, ma l'applicazione potrebbe essere rifiutata se non esiste una prova sostanziale che dimostra che i criteri sono soddisfatti (con una spiegazione):

1. Il prefisso ID del pacchetto identifica in modo corretto e chiaro il proprietario del pacchetto?

1. Il proprietario del pacchetto [ha abilitato l'autenticazione a due fattori per l'account NuGet.org](individual-accounts.md#enable-two-factor-authentication-2fa)?

1. Al prefisso ID del pacchetto fa riferimento un numero significativo di pacchetti già inviati dal proprietario?

1. Il prefisso ID del pacchetto è un elemento comune che non deve appartenere a un singolo proprietario o una sola organizzazione?

1. *Non* prenotare il prefisso ID del pacchetto può causare ambiguità e confusione per la community?

1. Le proprietà di identificazione dei pacchetti che corrispondono al prefisso ID del pacchetto sono chiare e coerenti (in particolare l'autore del pacchetto)?

1. I pacchetti hanno una licenza (usano l'elemento dei metadati [license](../reference/nuspec.md#license) e NON licenseUrl che sarà deprecato)?

1. Se i pacchetti hanno un'icona (usando l'elemento dei metadati iconUrl), usano anche l'elemento di metadati [Icon](../reference/nuspec.md#icon) (non è necessario rimuovere iconUrl)?

## <a name="third-party-feed-provider-scenarios"></a>Scenari di provider di feed di terze parti

Se un provider di feed di terze parti è interessato a implementare il proprio servizio per la prenotazione dei prefissi, è possibile modificare il servizio di ricerca nel provider di feed NuGet V3. La modifica del servizio di ricerca di feed consiste nell'aggiungere la proprietà *verified* con gli esempi per i feed V3 riportati di seguito. Il client di NuGet non supporta la proprietà aggiunta nel feed V2.

Per altre informazioni, consultare la [documentazione relativa al servizio di ricerca dell'API](../api/search-query-service-resource.md).

## <a name="package-id-prefix-reservation-dispute-policy"></a>Criteri per le controversie relative alla prenotazione del prefisso ID del pacchetto
Se si ritiene che a un proprietario in [NuGet.org](https://www.nuget.org) sia stata assegnata una prenotazione del prefisso ID del pacchetto che non è conforme ai criteri elencati sopra o viola diritti di marchi o copyright, inviare un messaggio di posta elettronica a [support@nuget.org](mailto:support@nuget.org) indicando il prefisso ID in questione, il proprietario del prefisso ID e il motivo per cui si contesta la prenotazione del prefisso assegnata.

