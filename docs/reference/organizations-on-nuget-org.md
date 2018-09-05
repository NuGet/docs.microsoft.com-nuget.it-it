---
title: Organizzazioni in nuget.org
description: Le organizzazioni in nuget.org aiuta a gestire i pacchetti pubblicati dal gruppo o in un team, l'ambiente aziendale.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: ea1ca607f169cd31c0a1b59d575d1a743763420c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551228"
---
# <a name="organization-on-nugetorg"></a>Organizzazione su nuget.org

Le organizzazioni consentono alle aziende e progetti open source per collaborare sui pacchetti tramite un'identità singola nuget.org. Per un utente del pacchetto, un account aziendale viene visualizzato come un account utente esistente in nuget.org.

## <a name="user-accounts-vs-organization-accounts"></a>Account utente e gli account dell'organizzazione

L'account utente è la tua identità su nuget.org e può essere un membro di un numero qualsiasi di organizzazioni. Un pacchetto può appartenere a un account aziendale, ad esempio può appartenere a un account utente. I consumer di pacchetti non vedono alcuna differenza tra un account utente o l'account dell'organizzazione: entrambi vengono visualizzati come pacchetto `owners`.

Un account dell'organizzazione ha uno o più account utente come relativi membri. Questi membri possono gestire un set di pacchetti mantenendo un'unica identità per la proprietà.

## <a name="adding-a-new-organization"></a>Aggiunta di una nuova organizzazione

Per aggiungere una nuova organizzazione, selezionare il proprio account in nuget.org, quindi selezionare il **alle organizzazioni di gestire...**  comando di menu:

![Opzione di menu su nuget.org per le organizzazioni di gestione](media/org-manage-option.png)

Nella pagina successiva selezionare il **Aggiungi nuova organizzazione** pulsante:

![Pulsante per creare una nuova organizzazione su nuget.org](media/org-add-new-option.png)

Nella pagina successiva, specificare l'indirizzo di posta elettronica e nome dell'organizzazione. Poiché gli account dell'organizzazione condividono lo stesso spazio dei nomi come account utente, il nome dell'organizzazione deve essere diverso da qualsiasi altra organizzazione esistente o gli account utente. L'indirizzo di posta elettronica deve inoltre essere univoco in tutti gli account.

![Aggiungi nuova organizzazione pagina su nuget.org](media/org-add-new-page.png)

Dopo aver creato l'account dell'organizzazione, si è l'amministratore può inviare pacchetti per l'organizzazione e aggiungere i membri dell'organizzazione.

### <a name="transform-existing-account-to-an-organization"></a>Trasformare un account esistente a un'organizzazione

> [!Warning]
> La conversione a account è un'operazione irreversibile: non è possibile trasformare un'organizzazione nuovamente a un account utente.

Se si gestiscono i pacchetti come team con un singolo account utente e si vuole convertire tale account in un'organizzazione, usare il **trasformare l'account a un'organizzazione** opzione di **gestire organizzazioni** pagina:

![Opzione su nuget.org per trasformare un account esistente da un'organizzazione](media/org-transform-option.png)

Nella pagina successiva specificare account utente diverso per assegnare come l'amministratore dell'organizzazione, quindi selezionare **trasformare**.

![Immissione delle informazioni per la trasformazione di un account utente in un'organizzazione](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Gestione dei membri dell'organizzazione

Come l'amministratore dell'organizzazione, è possibile aggiungere i membri, fornendo nuget.org ogni membro *nome dell'account utente*; non è possibile usare indirizzi di posta elettronica. Quindi si contrassegna ogni membro come un collaboratore o amministratore con le autorizzazioni seguenti:

| Autorizzazioni | Collaboratore | Amministratore |
| --- | --- | --- |
| Gestire i pacchetti dell'organizzazione<br/>(inviare nuovi pacchetti, aggiornare o rimuovere dall'elenco dei pacchetti esistenti) | Yes | Yes |
| Metadati di Change organizzazione<br/>(indirizzo di posta elettronica, le impostazioni di notifica) | No | Yes |
| Gestire i membri dell'organizzazione | No | Yes |
| Richiedere o eseguire operazioni su richieste comproprietà per i pacchetti dell'organizzazione | No | Yes |

## <a name="managing-packages"></a>La gestione dei pacchetti

È possibile visualizzare tutti i pacchetti per l'account e tutte le organizzazioni di cui si è un membro nel [Gestisci pacchetti](https://www.nuget.org/account/Packages) pagina. Per visualizzare i pacchetti specifici per l'account o da qualsiasi organizzazione specifico, usare il filtro degli account in alto a destra della pagina.

![La gestione dei pacchetti con il filtro di account](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Il trasferimento dei pacchetti a un'organizzazione
Se si vuole trasferire alcuni pacchetti a un'organizzazione appena creata, è possibile farlo richiede l'account dell'organizzazione al CO-proprietari del pacchetto e quindi rimuovere se stesso come proprietario. Se sei un amministratore dell'organizzazione, non vi è alcuna conferma necessaria per accettare la proprietà. Tuttavia, se sei un collaboratore, aggiungendo l'organizzazione come un proprietario richiede uno degli amministratori per accettare la proprietà.

## <a name="publishing-packages"></a>Pubblicazione di pacchetti

Pubblicazione dei pacchetti in un'organizzazione, ad esempio si pubblicano i pacchetti in un account utente: caricando direttamente il pacchetto in nuget.org o eseguendo il push del pacchetto il `nuget push` o `dotnet nuget push` i comandi dell'interfaccia della riga.

### <a name="uploading-packages"></a>Il caricamento dei pacchetti

Quando si carica direttamente un nuovo pacchetto nel [nuget.org caricamento](https://www.nuget.org/packages/manage/upload) pagina si assegna il proprietario del pacchetto a un account utente o l'organizzazione:

![Carica pacchetto con l'opzione relativa all'account](media/org-upload-option.png)

### <a name="using-api-keys"></a>Usando le chiavi API

Eseguire il push di un pacchetto il `nuget push` o `dotnet nuget push` comandi CLI, è necessario ottenere una chiave API necessaria per tali comandi. Per informazioni dettagliate, vedere [pubblicare un pacchetto](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).

Quando si crea una nuova chiave API, selezionare l'organizzazione appropriato nel **proprietario del pacchetto** elenco a discesa. Qualsiasi chiave API creata è applicabile solo per l'organizzazione scelto:

![Chiave API con l'opzione relativa all'account](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Rimozione di un'organizzazione

Come un utente, è possibile rimuovere se stessi da un'organizzazione selezionando il `X` pulsante visualizzato per l'appartenenza dell'organizzazione:

![Rimozione di un account utente da un'organizzazione](media/org-remove-self-option.png)

Gli amministratori possono rimuovere tutti i membri dell'organizzazione, inclusi altri amministratori. Se sei l'unico amministratore per un'organizzazione, è possibile rimuovere se stessi a meno che non si aggiunge un altro membro come amministratore.

### <a name="deleting-an-organization-account"></a>L'eliminazione di un account aziendale

Questa funzionalità sarà presto disponibile.
