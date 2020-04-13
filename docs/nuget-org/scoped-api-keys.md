---
title: Chiavi API con ambito
description: Assumere il controllo delle chiavi API da usare per eseguire il push dei pacchetti
author: mikejo5000
ms.author: mikejo
ms.date: 06/04/2019
ms.topic: conceptual
ms.openlocfilehash: 12d12d5294a474c4d3e4f5d3cad468bb515d21d5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "67426946"
---
# <a name="scoped-api-keys"></a>Chiavi API con ambito

Per fare di NuGet un ambiente più sicuro per la distribuzione dei pacchetti, è possibile assumere il controllo delle chiavi API tramite l'aggiunta di ambiti.

La possibilità di fornire l'ambito alle chiavi API garantisce un maggior controllo sulle API. È possibile:

- Creare più chiavi API con ambito che possono essere usate per diversi pacchetti con date di scadenza variabili.
- Ottenere le chiavi API in modo sicuro.
- Modificare le chiavi API esistenti per cambiare l'applicabilità di pacchetto.
- Aggiornare o eliminare le chiavi API esistenti senza intralciare le operazioni che usano altre chiavi.

## <a name="why-do-we-support-scoped-api-keys"></a>Perché sono supportate le chiavi API con ambito?

Gli ambiti per le chiavi API sono supportati per rendere disponibili autorizzazioni più dettagliate. In precedenza NuGet offriva un'unica chiave API per un account, e tale approccio presentava diversi inconvenienti:

- **Una sola chiave API per controllare tutti i pacchetti**. Con una sola chiave API per la gestione di tutti i pacchetti, è difficile condividere in modo sicuro la chiave quando più sviluppatori lavorano su pacchetti diversi e condividono un account editore.
- **Tutte le autorizzazioni o nessuna autorizzazione**. Chiunque abbia accesso alla chiave API dispone di tutte le autorizzazioni per i pacchetti (pubblicazione, push e rimozione dall'elenco). In molti casi questa situazione non è ottimale in un ambiente con più team.
- **Singolo punto di errore**. Un'unica chiave API significa anche un singolo punto di guasto. Se la chiave viene compromessa, tutti i pacchetti associati all'account potrebbero risultare compromessi. L'aggiornamento della chiave API è l'unico modo per risolvere il problema ed evitare un'interruzione del flusso di lavoro CI/CD. Possono anche esistere casi in cui si vuole revocare l'accesso alla chiave API per un utente (ad esempio quando un dipendente lascia l'organizzazione). Al momento non esiste un metodo ben definito per gestire questa situazione.

Con le chiavi API con ambito si tenta di risolvere questi problemi, assicurandosi nel contempo che nessuno dei flussi di lavoro esistenti interrompa l'esecuzione.

## <a name="acquire-an-api-key"></a>Acquisire una chiave API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a>Creare chiavi API con ambito

È possibile creare più chiavi API in base alle esigenze. Una chiave API può essere applicata a uno o più pacchetti, avere ambiti diversi che concedono privilegi specifici ed essere associata a una data di scadenza specifica.

Nell'esempio seguente la chiave API con nome `Contoso service CI` può essere usata per eseguire il push di pacchetti per pacchetti `Contoso.Service` specifici ed è valida per 365 giorni. Si tratta di uno scenario tipico in cui diversi team all'interno della stessa organizzazione lavorano su pacchetti diversi e i membri del team vengono dotati della chiave che concede loro privilegi solo per il pacchetto su cui stanno lavorando. La scadenza viene usata come meccanismo per evitare la presenza di chiavi non aggiornate o dimenticate.

![Creare chiavi API](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a>Usare i criteri GLOB

Se si sta lavorando su più pacchetti e si ha un lungo elenco di pacchetti da gestire, è possibile scegliere di usare i criteri GLOB per selezionare più pacchetti contemporaneamente. Se ad esempio si vuole concedere a una chiave ambiti specifici per tutti i pacchetti il cui ID inizia con `Fabrikam.Service`, è possibile eseguire questa operazione specificando `fabrikam.service.*` nella casella di testo del **criterio Glob**.

![Creare chiavi API](media/scoped-api-keys-glob-pattern.png)

L'uso di criteri GLOB per determinare le autorizzazioni della chiave API è valido anche per i nuovi pacchetti corrispondenti al criterio GLOB. Ad esempio, se si tenta di eseguire il push di un nuovo pacchetto denominato `Fabrikam.Service.Framework`, è possibile farlo con la chiave creata in precedenza, perché il pacchetto corrisponde al criterio GLOB `fabrikam.service.*`.

## <a name="obtain-api-keys-securely"></a>Ottenere le chiavi API in modo sicuro

Per la sicurezza, una chiave appena creata non viene mai visualizzata sullo schermo ed è disponibile unicamente tramite il pulsante **Copia**. Analogamente la chiave non è accessibile dopo l'aggiornamento della pagina.

![Creare chiavi API](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a>Modificare chiavi API esistenti

È anche possibile che si voglia aggiornare le autorizzazioni e gli ambiti per le chiavi senza modificare le chiavi stesse. Se si ha una chiave con uno o più ambiti specifici per un singolo pacchetto, è possibile scegliere di applicare lo stesso ambito o gli stessi ambiti su uno o molti altri pacchetti.

![Creare chiavi API](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a>Aggiornare o eliminare chiavi API esistenti

Il proprietario dell'account può scegliere di aggiornare la chiave, nel qual caso l'autorizzazione (per i pacchetti), l'ambito e la scadenza rimangono invariati, ma viene emessa una nuova chiave e la chiave precedente diventa inutilizzabile. Questo è utile per la gestione delle chiavi non aggiornate o nei casi in cui esiste il rischio di perdita di chiavi API.

![Creare chiavi API](media/scoped-api-keys-refresh.png)

È anche possibile scegliere di eliminare queste chiavi se non sono più necessarie. Se si elimina una chiave, questa viene rimossa e diventa inutilizzabile.

## <a name="faqs"></a>Domande frequenti

### <a name="what-happens-to-my-old-legacy-api-key"></a>Che cosa accade alla chiave API precedente (legacy)?

La chiave API precedente (legacy) continua a funzionare e può funzionare fino a quando si vuole usarla. Tuttavia queste chiavi vengono ritirate se non sono state usate da più di 365 giorni per eseguire il push di un pacchetto. Per altre informazioni, vedere il post di blog [Changes to expiring API keys](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html) (Modifiche per le chiavi API in scadenza). Questa chiave non può più essere aggiornata. È necessario eliminare la chiave legacy e creare una nuova chiave con ambito.

> [!NOTE]
> Questa chiave ha tutte le autorizzazioni per tutti i pacchetti e non scade mai. È consigliabile eliminare questa chiave e creare nuove chiavi dotate di autorizzazioni con ambito e scadenza definita.

### <a name="how-many-api-keys-can-i-create"></a>Quante chiavi API è possibile creare?

Non c'è limite al numero di chiavi API che è possibile creare. Tuttavia è consigliabile mantenere un numero di chiavi gestibile, per non avere molte chiavi non aggiornate e non riuscire a controllare da chi e dove vengono usate.

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a>È possibile eliminare la chiave API legacy o interromperne l'uso ora?

Sì. È possibile, ed è probabilmente necessario, eliminare la chiave API legacy.

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a>È possibile riottenere una chiave API eliminata per errore?

No. Dopo aver eliminato una chiave, è solo possibile creare nuove chiavi. Non è possibile recuperare le chiavi eliminate accidentalmente.

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a>La chiave API precedente continua a funzionare dopo l'aggiornamento della chiave API?

No. Quando si aggiorna una chiave, viene generata una nuova chiave con lo stesso ambito, la stessa autorizzazione e la stessa scadenza della chiave precedente. La chiave precedente cessa di esistere.

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a>È possibile concedere più autorizzazioni a una chiave API esistente?

Non è possibile modificare l'ambito, ma è possibile modificare l'elenco dei pacchetti ai quali la chiave è applicabile.

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a>Come si capisce se una delle proprie chiavi è scaduta o sta per scadere?

Se una qualsiasi chiave scade viene visualizzato un messaggio di avviso nella parte superiore della pagina. Viene anche inviato un avviso tramite posta elettronica al titolare dell'account dieci giorni prima della scadenza della chiave, per consentire l'adozione delle misure necessarie con il dovuto anticipo.