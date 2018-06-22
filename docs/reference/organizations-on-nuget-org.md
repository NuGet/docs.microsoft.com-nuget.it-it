---
title: Organizzazioni in nuget.org
description: Le organizzazioni in nuget.org aiuta a gestire i pacchetti pubblicati dal gruppo o in un team, l'ambiente aziendale.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 7f40654a08ac221c5ec3a90c86387b6760b28994
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2018
ms.locfileid: "34449578"
---
# <a name="organization-on-nugetorg"></a>Organizzazione in nuget.org

Le organizzazioni consentono alle aziende e progetti open source per collaborare sui pacchetti utilizzando un'identità nuget.org singolo. Per un consumer di pacchetto, un account aziendale viene visualizzato come un account utente esistenti in nuget.org.

## <a name="user-accounts-vs-organization-accounts"></a>Account utente e gli account dell'organizzazione

L'account utente è la tua identità in nuget.org e può essere un membro di un numero qualsiasi di organizzazioni. Un pacchetto può appartenere a un account aziendale, ad esempio può appartenere a un account utente. I consumer di pacchetto non vedranno alcuna differenza tra un account utente o l'account dell'organizzazione: entrambi vengono visualizzati come pacchetto `owners`.

Un account aziendale ha uno o più account utente come relativi membri. Questi membri possono gestire un set di pacchetti mantenendo una singola identità per la proprietà.

## <a name="adding-a-new-organization"></a>Aggiunta di una nuova organizzazione

Per aggiungere una nuova organizzazione, selezionare l'account in nuget.org, quindi selezionare il **alle organizzazioni di gestire...**  comando di menu:

![Opzione di menu in nuget.org per le organizzazioni di gestione](media/org-manage-option.png)

Nella pagina successiva, selezionare il **aggiungere nuova organizzazione** pulsante:

![Pulsante per creare una nuova organizzazione in nuget.org](media/org-add-new-option.png)

Nella pagina successiva, fornire l'indirizzo di posta elettronica e nome dell'organizzazione. Poiché gli account dell'organizzazione condividono lo stesso spazio dei nomi come account utente, il nome dell'organizzazione deve essere diverso da qualsiasi altra organizzazione esistente o gli account utente. L'indirizzo di posta elettronica deve essere univoco tra tutti gli account.

![Aggiungi nuova pagina di organizzazione in nuget.org](media/org-add-new-page.png)

Una volta creato l'account dell'organizzazione, si è l'amministratore può inviare i pacchetti per l'organizzazione e aggiunge membri dell'organizzazione.

### <a name="transform-existing-account-to-an-organization"></a>Trasformare un account esistente di un'organizzazione

> [!Warning]
> Conversione di account non può essere annullata: non è possibile trasformare un'organizzazione nuovamente a un account utente.

Se si gestiscono i pacchetti in team con un unico account utente e si desidera convertire quell'account in un'organizzazione, usare il **trasformare l'account a un'organizzazione** opzione il **organizzazioni di gestire** pagina:

![Opzione in nuget.org per trasformare un account esistente di un'organizzazione](media/org-transform-option.png)

Nella pagina successiva specificare account utente diverso per assegnare come l'amministratore dell'organizzazione, quindi selezionare **trasformare**.

![Immissione delle informazioni per la trasformazione di un account utente da un'organizzazione](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Gestione dei membri dell'organizzazione

Come amministratore dell'organizzazione, è possibile aggiungere membri fornendo nuget.org ogni membro *nome dell'account utente*; non è possibile utilizzare indirizzi di posta elettronica. Quindi si contrassegna ogni membro come collaboratore o amministratore con le autorizzazioni seguenti:

| Autorizzazioni | Collaboratore | Amministratore |
| --- | --- | --- |
| Gestire i pacchetti dell'organizzazione<br/>(Invia nuovi pacchetti, aggiornare o esclusione dei pacchetti esistenti) | Yes | Yes |
| Metadati di Change organizzazione<br/>(indirizzo di posta elettronica, le impostazioni di notifica) | No | Yes |
| Gestire i membri dell'organizzazione | No | Yes |
| Richiedere o eseguire operazioni su richieste comproprietà per i pacchetti dell'organizzazione | No | Yes |

## <a name="managing-packages"></a>La gestione dei pacchetti

È possibile visualizzare tutti i pacchetti attraverso il proprio account e tutte le organizzazioni di cui si è un membro nel [Gestisci pacchetti](https://www.nuget.org/account/Packages) pagina. Per visualizzare i pacchetti specifici per l'account o di qualsiasi organizzazione specifico, utilizzare il filtro di account in alto a destra della pagina.

![La gestione dei pacchetti con il filtro di account](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Trasferimento dei pacchetti per un'organizzazione
Se si desidera trasferire alcuni dei pacchetti a un'organizzazione appena creata, è possibile farlo che richiede l'account dell'organizzazione da Comproprietario il pacchetto e quindi rimuovendo manualmente come proprietario. Se si è amministratore dell'organizzazione, non vi è alcuna conferma tenuta ad accettare la proprietà. Aggiunta dell'organizzazione come proprietario, tuttavia, se si è un collaboratore, richiede a uno degli amministratori per accettare la proprietà.

## <a name="publishing-packages"></a>Pubblicazione di pacchetti

Pubblicazione dei pacchetti in un'organizzazione come pubblicare i pacchetti in un account utente: caricando direttamente il pacchetto a nuget.org o trasferendo il pacchetto il `nuget push` o `dotnet nuget push` i comandi CLI.

### <a name="uploading-packages"></a>Caricamento di pacchetti

Quando si carica direttamente un nuovo pacchetto nel [nuget.org caricamento](https://www.nuget.org/packages/manage/upload) pagina, assegnare il proprietario del pacchetto a un account utente o dell'organizzazione:

![Carica il pacchetto con l'opzione relativa all'account](media/org-upload-option.png)

### <a name="using-api-keys"></a>Utilizzando le chiavi API

Effettuare il push di un pacchetto il `nuget push` o `dotnet nuget push` i comandi CLI, è necessario ottenere una chiave API necessaria per tali comandi. Per informazioni dettagliate, vedere [pubblichi un pacchetto](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).

Quando si crea una nuova chiave API, selezionare l'organizzazione appropriato nella **proprietario del pacchetto** elenco a discesa. Un tasto qualsiasi API che crei è applicabile solo per l'organizzazione scelto:

![Chiave API con l'opzione relativa all'account](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Rimozione di un'organizzazione

Come un utente, è possibile rimuovere manualmente da un'organizzazione selezionando il `X` pulsante visualizzato per l'iscrizione dell'organizzazione:

![Rimozione di un account utente da un'organizzazione](media/org-remove-self-option.png)

Gli amministratori possono rimuovere tutti i membri dell'organizzazione, inclusi altri amministratori. Se si è l'unico amministratore per un'organizzazione, è possibile rimuovere se stessi a meno che non si aggiunge un altro membro come amministratore.

### <a name="deleting-an-organization-account"></a>Eliminazione di un account dell'organizzazione

Questa funzionalità sarà presto disponibile.
