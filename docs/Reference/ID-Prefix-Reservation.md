---
title: Prefisso ID prenotazione riferimento | Documenti Microsoft
author: diverdan92
ms.author: diverdan92
manager: unniravindranathan
ms.date: 10/9/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 76c0bb7f-9aaf-4c09-b3fd-f6802f9dd602
description: "Descrizione della funzionalità prenotazione prefisso ID pacchetto e la Guida dell'autore."
keywords: ID del pacchetto NuGet, prefisso, la prenotazione
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.openlocfilehash: e94d1431667ec17347165ac0a3993c0b552e6a60
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="package-id-prefix-reservation"></a>Prenotazione di prefisso ID pacchetto
[NuGet.org](https://www.nuget.org/) e Visual Studio 2017 15,4 o versione successiva mostra un indicatore visivo per il modello di denominazione del prefisso pacchetti che vengono inviati dai proprietari con un prefisso dell'ID pacchetto riservato, purché il pacchetto corrisponde all'ID riservato. Il riferimento di seguito viene illustrato cosa comporta la prenotazione di prefisso ID e come applicare un proprietario per un prefisso dell'ID.

## <a name="what-is-package-id-prefix-reservation"></a>Che cos'è la prenotazione di prefisso ID pacchetto?
I proprietari del pacchetto sono in grado di riservare e proteggere la propria identità riservando prefissi ID. I consumer di pacchetto vengono fornite informazioni aggiuntive quando si utilizzano pacchetti che il pacchetto in uso non sono ingannevoli nelle relative proprietà di identificazione. Per vedere come prenotazione di prefisso ID funziona nei dettagli di lettura.

## <a name="id-prefix-reservation-details"></a>Dettagli di prenotazione prefisso ID 
Quando un prefisso dell'ID pacchetto è riservato, si verifica quanto riportato nel [nuget.org](https://www.nuget.org/) raccolta, come in Visual Studio. Inoltre, sono avanzate scenari supportati da prenotazioni prefisso ID, ad esempio l'impostazione di un prefisso come 'public', la delega di subset di prefisso a più proprietari.

La seguente sezione viene descritta la funzionalità in dettaglio, nonché le funzionalità più avanzate.

### <a name="id-prefix-reservation-on-nugetorg"></a>Prenotazione di prefisso ID su nuget.org
Quando un prefisso è riservato in [nuget.org](https://www.nuget.org/), si verificherà quanto segue:
1. Una prenotazione di prefisso è associata un proprietario o un set di proprietari in [nuget.org](https://www.nuget.org/). 
2. Ogni volta che un pacchetto viene inviato a [nuget.org](https://www.nuget.org/) con un ID che corrisponde al prefisso ID riservato, il pacchetto viene rifiutato, a meno che il codice ha origine il o i proprietari riservato il prefisso dell'ID.
3. I pacchetti che corrisponde al prefisso ID riservato e deriva da sui proprietari riservato il prefisso dell'ID avrà un indicatore visivo in Visual Studio 2017 15,4 o versione successiva e in [nuget.org](https://www.nuget.org/) che indica che il pacchetto è in prefisso ID riservato. Questo vale per gli invii di nuovo pacchetto nonché a sotto il o i proprietari dei pacchetti esistenti. **Nota:** l'indicatore in Visual Studio verrà visualizzata solo se è selezionato un singolo feed come origine del pacchetto. 
4. Tutti i pacchetti esistenti che soddisfano il prefisso dell'ID riservato, ma sono *non* il proprietario di riservato del prefisso rimarrà invariato (non saranno non in elenco, ma non avranno anche l'indicatore visivo). Inoltre, i proprietari dei pacchetti sarà comunque in grado di inviare nuove versioni del pacchetto.

Queste modifiche sono in base alle condizioni seguenti e impongano restrizioni aggiuntive diversi:
* Solo un proprietario di un pacchetto deve avere il prefisso riservato per l'indicatore visivo (per i pacchetti con più proprietari).
* Se è presente più di un proprietario di un pacchetto in cui uno o più proprietari è il prefisso riservato e uno o più proprietari non hanno il prefisso riservato, solo il proprietario con il prefisso riservato possibile rimuovere altri proprietari con un prefisso riservato. I proprietari che non hanno il prefisso riservato non è possibile rimuovere proprietari con il prefisso riservato. È comunque possibile rimuovere altri proprietari che inoltre, non hanno il prefisso riservato.
  * Una volta che un pacchetto contiene l'indicatore visivo, dovrebbe essere *sempre* hanno l'indicatore visivo (garantendo che almeno un proprietario con il prefisso riservato rimarrà sempre un proprietario)

### <a name="advanced-prefix-reservation-scenarios"></a>Scenari di prenotazione prefisso avanzate
Esistono diversi scenari prenotazione prefisso più avanzati descritti di seguito, tra cui subprefix delega e prefissi contrassegnato come pubblico. Di seguito sono riportati le prenotazioni di prefisso più avanzate che possono essere effettuate. 

* Durante la prenotazione di prefisso, il proprietario può richiedere la delega di subset di prefisso (o il prefisso) ad altri proprietari. Ad esempio, se '[Microsoft](https://www.nuget.org/profiles/microsoft)' proprietario ' Microsoft.\*', ma '[aspnet](https://www.nuget.org/profiles/aspnet)' desidera riservare ' Microsoft.AspNet.\*','[Microsoft](https://www.nuget.org/profiles/microsoft)' può essere scegliere di delegare ' Microsoft.AspNet. \*' per il [aspnet](https://www.nuget.org/profiles/aspnet) account.
*  Durante la prenotazione di prefisso, il proprietario è possibile scegliere di rendere pubblico un prefisso. Si continuerà a fornire loro l'indicatore visivo che mostra che il pacchetto proviene da un prefisso riservato, ma verrà **non** invii pacchetto futuri in base al prefisso per qualsiasi proprietario di blocco. Ciò è utile per i progetti di origine aperto con molti autori: i collaboratori alla parte superiore o core può avere il prefisso riservato, ma può comunque essere aperta a tutti i collaboratori. 

### <a name="prefix-reservation-visual-indicator"></a>Indicatore visivo della prenotazione di prefisso
Quando un pacchetto proviene da un prefisso riservato, verrà visualizzato di seguito indicatori visivi nel [nuget.org](https://www.nuget.org/) raccolta e in Visual Studio 2017 15,4 o versione successiva:

**Raccolta di NuGet.org**
![nuget.org raccolta](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Processo dell'applicazione di prenotazione prefisso ID
Per richiedere una prenotazione di prefisso, seguire i passaggi seguenti. 
1. Esaminare l'accettazione [criteri per la prenotazione di prefisso ID](#id-prefix-reservation-criteria).
2. Determinare gli spazi dei nomi che si desidera riservare, oltre a qualsiasi [prefisso prenotazione scenari avanzati](#advanced-prefix-reservation-scenarios) potrebbero essere necessarie.
3. Inviare un messaggio a [ account@nuget.org ](mailto:account@nuget.org) con il proprietario del nome visualizzato in [nuget.org](https://www.nuget.org/), nonché qualsiasi prefisso riservato richiesto. Delegare subset prefisso a più proprietari, assicurarsi che si menzionano tutti i nomi visualizzati di proprietario e prefisso subset.

Dopo l'applicazione è stata inviata, riceverà una notifica di accettazione o rifiuto (con i criteri che ha causato il rifiuto). È possibile che sia necessario per porre domande di identificazione aggiuntive per verificare l'identità del proprietario. 

### <a name="id-prefix-reservation-criteria"></a>Criterio di prenotazione prefisso ID
Durante la revisione di qualsiasi applicazione per la prenotazione di prefisso ID, il [nuget.org](https://www.nuget.org/) team verrà evalaute l'applicazione in base il di sotto di criteri. Non tutti i criteri deve essere soddisfatta per un prefisso a essere riservato, ma potrebbe non essere consentito l'applicazione se non c'è notevole evidenza dei criteri in grado di soddisfare (con una spiegazione di base):
1. Il prefisso dell'ID pacchetto correttamente e chiaramente identifica il proprietario del pacchetto?
2. Sono un numero significativo di pacchetti che sono già state inviate dal proprietario con il prefisso dell'ID pacchetto?
3. Il prefisso dell'ID pacchetto è un elemento comune che non devono appartenere a qualsiasi singolo proprietario o organizzazione?
4. Sarebbe *non* riservare il prefisso dell'ID pacchetto causare ambiguità e confusione per la community?
5. Sono le proprietà di identificazione dei pacchetti che corrispondono al pacchetto ID prefisso chiaro e coerente (in particolare l'autore del pacchetto)?

## <a name="3rd-party-feed-provider-scenarios"></a>scenari di provider di feed 3rd party
Se una parte 3 di provider di feed è l'implementazione i propri servizi per fornire le prenotazioni di prefisso, è possibile effettuare questa operazione modificando il servizio di ricerca nello NuGet V3 feed provider. L'aggiunta del servizio di ricerca di feed consiste nell'aggiungere il *verificato* proprietà, con gli esempi per i feed V3 riportato di seguito. Il client NuGet non supporta la proprietà aggiunta il v2 feed.

Per ulteriori informazioni, vedere il [documentazione sul servizio di ricerca dell'API](../api/search-query-service-resource.md).
