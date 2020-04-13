---
title: Organizzazione in NuGet.org
description: Le organizzazioni in NuGet.org consentono di gestire pacchetti pubblicati dal gruppo o in un team in un ambiente aziendale.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427076"
---
# <a name="your-organization-on-nugetorg"></a>Organizzazione in NuGet.org

Le organizzazioni consentono ad aziende e progetti open source di gestire i pacchetti tramite un'unica identità NuGet.org. Per un consumer di pacchetti, un account aziendale equivale a un account utente esistente in NuGet.org.

## <a name="organization-accounts-vs-individual-accounts"></a>Account aziendali e account personali

Un account aziendale ha uno o più account (utente) personali come membri. Questi membri possono gestire un set di pacchetti mantenendo un'unica identità per la proprietà.

L'account personale è l'identità dell'utente in NuGet.org e può essere membro di un numero qualsiasi di organizzazioni. Un pacchetto può appartenere a un account aziendale come a un account individuale. I consumer di pacchetti non notano differenze tra un account personale e l'account aziendale: entrambi vengono visualizzati come `owners` del pacchetto.

## <a name="adding-a-new-organization"></a>Aggiunta di una nuova organizzazione

Per aggiungere una nuova organizzazione, selezionare l'account in NuGet.org, quindi selezionare il comando di menu **Manage Organizations...** (Gestisci organizzazioni):

![Opzione di menu in NuGet.org per la gestione delle organizzazioni](media/org-manage-option.png)

Nella pagina successiva selezionare il pulsante **Add new organization** (Aggiungi nuova organizzazione):

![Pulsante per creare una nuova organizzazione in NuGet.org](media/org-add-new-option.png)

Nella pagina successiva specificare il nome dell'organizzazione e l'indirizzo di posta elettronica. Poiché gli account aziendali condividono lo stesso spazio dei nomi degli account utente, il nome dell'organizzazione deve essere diverso da qualsiasi altro account aziendale o utente esistente. Anche l'indirizzo di posta elettronica deve essere univoco in tutti gli account.

![Pagina per aggiungere una nuova organizzazione in NuGet.org](media/org-add-new-page.png)

Dopo aver creato l'account aziendale, l'utente diventa amministratore e può inviare pacchetti per l'organizzazione e aggiungere membri dell'organizzazione.

### <a name="transform-existing-account-to-an-organization"></a>Trasformare un account esistente in un'organizzazione

> [!Warning]
> La conversione dell'account è un'operazione irreversibile. Non è possibile trasformare un'organizzazione nuovamente in un account utente.

Se si gestiscono i pacchetti come team usando un unico account utente e si vuole convertire tale account in un'organizzazione, usare l'opzione **Transform your account to an organization** (Trasforma l'account in un'organizzazione) nella pagina **Manage Organizations** (Gestisci organizzazioni):

![Opzione in NuGet.org per trasformare un account esistente in un'organizzazione](media/org-transform-option.png)

Nella pagina successiva specificare un account utente diverso per assegnare l'amministratore dell'organizzazione, quindi selezionare **Transform** (Trasforma).

![Immissione delle informazioni per la trasformazione di un account utente in un'organizzazione](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Gestione di membri dell'organizzazione

L'amministratore dell'organizzazione può aggiungere membri specificando il *nome dell'account utente* NuGet.org di ogni membro. Non è possibile usare indirizzi di posta elettronica. Ogni membro viene poi contrassegnato come collaboratore o amministratore con le autorizzazioni seguenti:

| Autorizzazione | Collaboratore | Amministratore |
| --- | --- | --- |
| Gestire i pacchetti dell'organizzazione<br/>(inviare nuovi pacchetti, aggiornare o rimuovere dall'elenco pacchetti esistenti) | Sì | Sì |
| Modificare i metadati dell'organizzazione<br/>(indirizzi di posta elettronica, impostazioni di notifica) | No | Sì |
| Gestire i membri dell'organizzazione | No | Sì |
| Richiedere o gestire richieste di comproprietà per pacchetti dell'organizzazione | No | Sì |

## <a name="managing-packages"></a>Gestione di pacchetti

È possibile visualizzare tutti i pacchetti dell'account e di tutte le organizzazioni di cui si è membro nella pagina [Manage Packages](https://www.nuget.org/account/Packages) (Gestisci pacchetti). Per visualizzare i pacchetti specifici dell'account o di una qualsiasi organizzazione, usare il filtro di account nella parte superiore destra della pagina.

![Gestione di pacchetti con il filtro di account](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Trasferimento di pacchetti a un'organizzazione
Se si vogliono trasferire alcuni pacchetti a un'organizzazione appena creata, è necessario richiedere l'account aziendale per diventare comproprietari del pacchetto e rimuovere se stesso come proprietario. Se si è amministratore dell'organizzazione, non è necessaria una conferma di accettazione della proprietà. Se si è invece collaboratore, per poter aggiungere l'organizzazione come proprietario è necessario che uno degli amministratori accetti la proprietà.

## <a name="publishing-packages"></a>Pubblicazione di pacchetti

I pacchetti vengono pubblicati in un'organizzazione esattamente con in un account utente. È possibile caricare il pacchetto direttamente in NuGet.org oppure pubblicarlo tramite i comandi dell'interfaccia della riga di comando `nuget push` o `dotnet nuget push`.

### <a name="uploading-packages"></a>Caricamento di pacchetti

Quando si carica direttamente un nuovo pacchetto nella pagina [Upload](https://www.nuget.org/packages/manage/upload) (Carica ) di NuGet.org, si assegna il proprietario del pacchetto a un account utente o aziendale:

![Caricare un pacchetto con l'opzione account](media/org-upload-option.png)

### <a name="using-api-keys"></a>Uso di chiavi API

Per eseguire il push di un pacchetto tramite i comandi dell'interfaccia della riga di comando `nuget push` o `dotnet nuget push`, è necessario ottenere una chiave API richiesta da tali comandi. Per informazioni dettagliate, vedere [Pubblicare un pacchetto](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).

Quando si crea una nuova chiave API, selezionare l'organizzazione appropriata nell'elenco a discesa **Package Owner** (Proprietario pacchetto). Le chiavi API create sono applicabili solo all'organizzazione selezionata:

![Chiave API con opzione account](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Uscita da un'organizzazione

Un utente può uscire da un'organizzazione selezionando il pulsante **X** visualizzato dall'appartenenza all'organizzazione:

![Rimozione di un account utente da un'organizzazione](media/org-remove-self-option.png)

Gli amministratori possono rimuovere tutti i membri dell'organizzazione, inclusi altri amministratori. Se si è il solo amministratore di un'organizzazione, non è possibile rimuovere se stessi a meno che non si aggiunga un altro membro come amministratore.

### <a name="deleting-an-organization-account"></a>Eliminazione di un account aziendale

È possibile eliminare un account aziendale facendo clic sul pulsante **Delete** (Elimina) visualizzato nella pagina dell'organizzazione.

![Eliminazione di un'organizzazione](media/org-delete-option.png)

Per eliminare l'organizzazione, confermare l'operazione facendo clic sul pulsante di conferma **Delete organization** (Elimina organizzazione).
