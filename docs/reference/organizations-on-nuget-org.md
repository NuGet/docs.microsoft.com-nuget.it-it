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
# <a name="organization-on-nugetorg"></a><span data-ttu-id="03440-103">Organizzazione su nuget.org</span><span class="sxs-lookup"><span data-stu-id="03440-103">Organization on nuget.org</span></span>

<span data-ttu-id="03440-104">Le organizzazioni consentono alle aziende e progetti open source per collaborare sui pacchetti tramite un'identità singola nuget.org.</span><span class="sxs-lookup"><span data-stu-id="03440-104">Organizations enable businesses and open-source projects to collaborate on packages using a single nuget.org identity.</span></span> <span data-ttu-id="03440-105">Per un utente del pacchetto, un account aziendale viene visualizzato come un account utente esistente in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="03440-105">For a package consumer, an organization account appears same as an existing user account on nuget.org.</span></span>

## <a name="user-accounts-vs-organization-accounts"></a><span data-ttu-id="03440-106">Account utente e gli account dell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="03440-106">User accounts vs. organization accounts</span></span>

<span data-ttu-id="03440-107">L'account utente è la tua identità su nuget.org e può essere un membro di un numero qualsiasi di organizzazioni.</span><span class="sxs-lookup"><span data-stu-id="03440-107">Your user account is your identity on nuget.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="03440-108">Un pacchetto può appartenere a un account aziendale, ad esempio può appartenere a un account utente.</span><span class="sxs-lookup"><span data-stu-id="03440-108">A package can belong to an organization account like it can belong to a user account.</span></span> <span data-ttu-id="03440-109">I consumer di pacchetti non vedono alcuna differenza tra un account utente o l'account dell'organizzazione: entrambi vengono visualizzati come pacchetto `owners`.</span><span class="sxs-lookup"><span data-stu-id="03440-109">Package consumers don't see any difference between an user account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="03440-110">Un account dell'organizzazione ha uno o più account utente come relativi membri.</span><span class="sxs-lookup"><span data-stu-id="03440-110">An organization account has one or more user accounts as its members.</span></span> <span data-ttu-id="03440-111">Questi membri possono gestire un set di pacchetti mantenendo un'unica identità per la proprietà.</span><span class="sxs-lookup"><span data-stu-id="03440-111">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="03440-112">Aggiunta di una nuova organizzazione</span><span class="sxs-lookup"><span data-stu-id="03440-112">Adding a new organization</span></span>

<span data-ttu-id="03440-113">Per aggiungere una nuova organizzazione, selezionare il proprio account in nuget.org, quindi selezionare il **alle organizzazioni di gestire...**  comando di menu:</span><span class="sxs-lookup"><span data-stu-id="03440-113">To add a new organization, select your account on nuget.org, then select the **Manage Organizations...** menu command:</span></span>

![Opzione di menu su nuget.org per le organizzazioni di gestione](media/org-manage-option.png)

<span data-ttu-id="03440-115">Nella pagina successiva selezionare il **Aggiungi nuova organizzazione** pulsante:</span><span class="sxs-lookup"><span data-stu-id="03440-115">On the next page, select the **Add new organization** button:</span></span>

![Pulsante per creare una nuova organizzazione su nuget.org](media/org-add-new-option.png)

<span data-ttu-id="03440-117">Nella pagina successiva, specificare l'indirizzo di posta elettronica e nome dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="03440-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="03440-118">Poiché gli account dell'organizzazione condividono lo stesso spazio dei nomi come account utente, il nome dell'organizzazione deve essere diverso da qualsiasi altra organizzazione esistente o gli account utente.</span><span class="sxs-lookup"><span data-stu-id="03440-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="03440-119">L'indirizzo di posta elettronica deve inoltre essere univoco in tutti gli account.</span><span class="sxs-lookup"><span data-stu-id="03440-119">The email address must also be unique across all accounts.</span></span>

![Aggiungi nuova organizzazione pagina su nuget.org](media/org-add-new-page.png)

<span data-ttu-id="03440-121">Dopo aver creato l'account dell'organizzazione, si è l'amministratore può inviare pacchetti per l'organizzazione e aggiungere i membri dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="03440-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="03440-122">Trasformare un account esistente a un'organizzazione</span><span class="sxs-lookup"><span data-stu-id="03440-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="03440-123">La conversione a account è un'operazione irreversibile: non è possibile trasformare un'organizzazione nuovamente a un account utente.</span><span class="sxs-lookup"><span data-stu-id="03440-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="03440-124">Se si gestiscono i pacchetti come team con un singolo account utente e si vuole convertire tale account in un'organizzazione, usare il **trasformare l'account a un'organizzazione** opzione di **gestire organizzazioni** pagina:</span><span class="sxs-lookup"><span data-stu-id="03440-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Opzione su nuget.org per trasformare un account esistente da un'organizzazione](media/org-transform-option.png)

<span data-ttu-id="03440-126">Nella pagina successiva specificare account utente diverso per assegnare come l'amministratore dell'organizzazione, quindi selezionare **trasformare**.</span><span class="sxs-lookup"><span data-stu-id="03440-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Immissione delle informazioni per la trasformazione di un account utente in un'organizzazione](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="03440-128">Gestione dei membri dell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="03440-128">Managing organization members</span></span>

<span data-ttu-id="03440-129">Come l'amministratore dell'organizzazione, è possibile aggiungere i membri, fornendo nuget.org ogni membro *nome dell'account utente*; non è possibile usare indirizzi di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="03440-129">As the organization administrator, you can add members by providing each member's nuget.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="03440-130">Quindi si contrassegna ogni membro come un collaboratore o amministratore con le autorizzazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="03440-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="03440-131">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="03440-131">Permission</span></span> | <span data-ttu-id="03440-132">Collaboratore</span><span class="sxs-lookup"><span data-stu-id="03440-132">Collaborator</span></span> | <span data-ttu-id="03440-133">Amministratore</span><span class="sxs-lookup"><span data-stu-id="03440-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="03440-134">Gestire i pacchetti dell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="03440-134">Manage the organization's packages</span></span><br/><span data-ttu-id="03440-135">(inviare nuovi pacchetti, aggiornare o rimuovere dall'elenco dei pacchetti esistenti)</span><span class="sxs-lookup"><span data-stu-id="03440-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="03440-136">Yes</span><span class="sxs-lookup"><span data-stu-id="03440-136">Yes</span></span> | <span data-ttu-id="03440-137">Yes</span><span class="sxs-lookup"><span data-stu-id="03440-137">Yes</span></span> |
| <span data-ttu-id="03440-138">Metadati di Change organizzazione</span><span class="sxs-lookup"><span data-stu-id="03440-138">Change organization metadata</span></span><br/><span data-ttu-id="03440-139">(indirizzo di posta elettronica, le impostazioni di notifica)</span><span class="sxs-lookup"><span data-stu-id="03440-139">(email address, notification settings)</span></span> | <span data-ttu-id="03440-140">No</span><span class="sxs-lookup"><span data-stu-id="03440-140">No</span></span> | <span data-ttu-id="03440-141">Yes</span><span class="sxs-lookup"><span data-stu-id="03440-141">Yes</span></span> |
| <span data-ttu-id="03440-142">Gestire i membri dell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="03440-142">Manage organization members</span></span> | <span data-ttu-id="03440-143">No</span><span class="sxs-lookup"><span data-stu-id="03440-143">No</span></span> | <span data-ttu-id="03440-144">Yes</span><span class="sxs-lookup"><span data-stu-id="03440-144">Yes</span></span> |
| <span data-ttu-id="03440-145">Richiedere o eseguire operazioni su richieste comproprietà per i pacchetti dell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="03440-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="03440-146">No</span><span class="sxs-lookup"><span data-stu-id="03440-146">No</span></span> | <span data-ttu-id="03440-147">Yes</span><span class="sxs-lookup"><span data-stu-id="03440-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="03440-148">La gestione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="03440-148">Managing packages</span></span>

<span data-ttu-id="03440-149">È possibile visualizzare tutti i pacchetti per l'account e tutte le organizzazioni di cui si è un membro nel [Gestisci pacchetti](https://www.nuget.org/account/Packages) pagina.</span><span class="sxs-lookup"><span data-stu-id="03440-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="03440-150">Per visualizzare i pacchetti specifici per l'account o da qualsiasi organizzazione specifico, usare il filtro degli account in alto a destra della pagina.</span><span class="sxs-lookup"><span data-stu-id="03440-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![La gestione dei pacchetti con il filtro di account](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="03440-152">Il trasferimento dei pacchetti a un'organizzazione</span><span class="sxs-lookup"><span data-stu-id="03440-152">Transferring packages to an organization</span></span>
<span data-ttu-id="03440-153">Se si vuole trasferire alcuni pacchetti a un'organizzazione appena creata, è possibile farlo richiede l'account dell'organizzazione al CO-proprietari del pacchetto e quindi rimuovere se stesso come proprietario.</span><span class="sxs-lookup"><span data-stu-id="03440-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="03440-154">Se sei un amministratore dell'organizzazione, non vi è alcuna conferma necessaria per accettare la proprietà.</span><span class="sxs-lookup"><span data-stu-id="03440-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="03440-155">Tuttavia, se sei un collaboratore, aggiungendo l'organizzazione come un proprietario richiede uno degli amministratori per accettare la proprietà.</span><span class="sxs-lookup"><span data-stu-id="03440-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="03440-156">Pubblicazione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="03440-156">Publishing packages</span></span>

<span data-ttu-id="03440-157">Pubblicazione dei pacchetti in un'organizzazione, ad esempio si pubblicano i pacchetti in un account utente: caricando direttamente il pacchetto in nuget.org o eseguendo il push del pacchetto il `nuget push` o `dotnet nuget push` i comandi dell'interfaccia della riga.</span><span class="sxs-lookup"><span data-stu-id="03440-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to nuget.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="03440-158">Il caricamento dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="03440-158">Uploading packages</span></span>

<span data-ttu-id="03440-159">Quando si carica direttamente un nuovo pacchetto nel [nuget.org caricamento](https://www.nuget.org/packages/manage/upload) pagina si assegna il proprietario del pacchetto a un account utente o l'organizzazione:</span><span class="sxs-lookup"><span data-stu-id="03440-159">When you directly upload a new package on the [nuget.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Carica pacchetto con l'opzione relativa all'account](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="03440-161">Usando le chiavi API</span><span class="sxs-lookup"><span data-stu-id="03440-161">Using API keys</span></span>

<span data-ttu-id="03440-162">Eseguire il push di un pacchetto il `nuget push` o `dotnet nuget push` comandi CLI, è necessario ottenere una chiave API necessaria per tali comandi.</span><span class="sxs-lookup"><span data-stu-id="03440-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="03440-163">Per informazioni dettagliate, vedere [pubblicare un pacchetto](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="03440-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="03440-164">Quando si crea una nuova chiave API, selezionare l'organizzazione appropriato nel **proprietario del pacchetto** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="03440-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="03440-165">Qualsiasi chiave API creata è applicabile solo per l'organizzazione scelto:</span><span class="sxs-lookup"><span data-stu-id="03440-165">Any API key you create is applicable only to the chosen organization:</span></span>

![Chiave API con l'opzione relativa all'account](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="03440-167">Rimozione di un'organizzazione</span><span class="sxs-lookup"><span data-stu-id="03440-167">Removing an organization</span></span>

<span data-ttu-id="03440-168">Come un utente, è possibile rimuovere se stessi da un'organizzazione selezionando il `X` pulsante visualizzato per l'appartenenza dell'organizzazione:</span><span class="sxs-lookup"><span data-stu-id="03440-168">As a user, you can remove yourself from an organization by selecting the `X` button shown by your organization membership:</span></span>

![Rimozione di un account utente da un'organizzazione](media/org-remove-self-option.png)

<span data-ttu-id="03440-170">Gli amministratori possono rimuovere tutti i membri dell'organizzazione, inclusi altri amministratori.</span><span class="sxs-lookup"><span data-stu-id="03440-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="03440-171">Se sei l'unico amministratore per un'organizzazione, è possibile rimuovere se stessi a meno che non si aggiunge un altro membro come amministratore.</span><span class="sxs-lookup"><span data-stu-id="03440-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="03440-172">L'eliminazione di un account aziendale</span><span class="sxs-lookup"><span data-stu-id="03440-172">Deleting an organization account</span></span>

<span data-ttu-id="03440-173">Questa funzionalità sarà presto disponibile.</span><span class="sxs-lookup"><span data-stu-id="03440-173">This feature is coming soon.</span></span>
