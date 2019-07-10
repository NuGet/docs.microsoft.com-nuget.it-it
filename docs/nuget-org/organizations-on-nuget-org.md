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
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427076"
---
# <a name="your-organization-on-nugetorg"></a><span data-ttu-id="23943-103">Organizzazione in NuGet.org</span><span class="sxs-lookup"><span data-stu-id="23943-103">Your organization on NuGet.org</span></span>

<span data-ttu-id="23943-104">Le organizzazioni consentono ad aziende e progetti open source di gestire i pacchetti tramite un'unica identità NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="23943-104">Organizations enable businesses and open-source projects to collaborate on packages using a single NuGet.org identity.</span></span> <span data-ttu-id="23943-105">Per un consumer di pacchetti, un account aziendale equivale a un account utente esistente in NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="23943-105">For a package consumer, an organization account appears same as an existing user account on NuGet.org.</span></span>

## <a name="organization-accounts-vs-individual-accounts"></a><span data-ttu-id="23943-106">Account aziendali e account personali</span><span class="sxs-lookup"><span data-stu-id="23943-106">Organization accounts vs. individual accounts</span></span>

<span data-ttu-id="23943-107">Un account aziendale ha uno o più account (utente) personali come membri.</span><span class="sxs-lookup"><span data-stu-id="23943-107">An organization account has one or more individual (user) accounts as its members.</span></span> <span data-ttu-id="23943-108">Questi membri possono gestire un set di pacchetti mantenendo un'unica identità per la proprietà.</span><span class="sxs-lookup"><span data-stu-id="23943-108">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

<span data-ttu-id="23943-109">L'account personale è l'identità dell'utente in NuGet.org e può essere membro di un numero qualsiasi di organizzazioni.</span><span class="sxs-lookup"><span data-stu-id="23943-109">Your individual account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="23943-110">Un pacchetto può appartenere a un account aziendale come a un account personale.</span><span class="sxs-lookup"><span data-stu-id="23943-110">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="23943-111">I consumer di pacchetti non notano differenze tra un account personale e l'account aziendale: entrambi vengono visualizzati come `owners` del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="23943-111">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="23943-112">Aggiunta di una nuova organizzazione</span><span class="sxs-lookup"><span data-stu-id="23943-112">Adding a new organization</span></span>

<span data-ttu-id="23943-113">Per aggiungere una nuova organizzazione, selezionare l'account in NuGet.org, quindi selezionare il comando di menu **Manage Organizations...** (Gestisci organizzazioni):</span><span class="sxs-lookup"><span data-stu-id="23943-113">To add a new organization, select your account on NuGet.org, then select the **Manage Organizations...** menu command:</span></span>

![Opzione di menu in NuGet.org per la gestione delle organizzazioni](media/org-manage-option.png)

<span data-ttu-id="23943-115">Nella pagina successiva selezionare il pulsante **Add new organization** (Aggiungi nuova organizzazione):</span><span class="sxs-lookup"><span data-stu-id="23943-115">On the next page, select the **Add new organization** button:</span></span>

![Pulsante per creare una nuova organizzazione in NuGet.org](media/org-add-new-option.png)

<span data-ttu-id="23943-117">Nella pagina successiva specificare il nome dell'organizzazione e l'indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="23943-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="23943-118">Poiché gli account aziendali condividono lo stesso spazio dei nomi degli account utente, il nome dell'organizzazione deve essere diverso da qualsiasi altro account aziendale o utente esistente.</span><span class="sxs-lookup"><span data-stu-id="23943-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="23943-119">Anche l'indirizzo di posta elettronica deve essere univoco in tutti gli account.</span><span class="sxs-lookup"><span data-stu-id="23943-119">The email address must also be unique across all accounts.</span></span>

![Pagina per aggiungere una nuova organizzazione in NuGet.org](media/org-add-new-page.png)

<span data-ttu-id="23943-121">Dopo aver creato l'account aziendale, l'utente diventa amministratore e può inviare pacchetti per l'organizzazione e aggiungere membri dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="23943-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="23943-122">Trasformare un account esistente in un'organizzazione</span><span class="sxs-lookup"><span data-stu-id="23943-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="23943-123">La conversione dell'account è un'operazione irreversibile. Non è possibile trasformare un'organizzazione nuovamente in un account utente.</span><span class="sxs-lookup"><span data-stu-id="23943-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="23943-124">Se si gestiscono i pacchetti come team usando un unico account utente e si vuole convertire tale account in un'organizzazione, usare l'opzione **Transform your account to an organization** (Trasforma l'account in un'organizzazione) nella pagina **Manage Organizations** (Gestisci organizzazioni):</span><span class="sxs-lookup"><span data-stu-id="23943-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Opzione in NuGet.org per trasformare un account esistente in un'organizzazione](media/org-transform-option.png)

<span data-ttu-id="23943-126">Nella pagina successiva specificare un account utente diverso per assegnare l'amministratore dell'organizzazione, quindi selezionare **Transform** (Trasforma).</span><span class="sxs-lookup"><span data-stu-id="23943-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Immissione delle informazioni per la trasformazione di un account utente in un'organizzazione](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="23943-128">Gestione di membri dell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="23943-128">Managing organization members</span></span>

<span data-ttu-id="23943-129">L'amministratore dell'organizzazione può aggiungere membri specificando il *nome dell'account utente* NuGet.org di ogni membro. Non è possibile usare indirizzi di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="23943-129">As the organization administrator, you can add members by providing each member's NuGet.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="23943-130">Ogni membro viene poi contrassegnato come collaboratore o amministratore con le autorizzazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="23943-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="23943-131">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="23943-131">Permission</span></span> | <span data-ttu-id="23943-132">Collaboratore</span><span class="sxs-lookup"><span data-stu-id="23943-132">Collaborator</span></span> | <span data-ttu-id="23943-133">Amministratore</span><span class="sxs-lookup"><span data-stu-id="23943-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="23943-134">Gestire i pacchetti dell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="23943-134">Manage the organization's packages</span></span><br/><span data-ttu-id="23943-135">(inviare nuovi pacchetti, aggiornare o rimuovere dall'elenco pacchetti esistenti)</span><span class="sxs-lookup"><span data-stu-id="23943-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="23943-136">Sì</span><span class="sxs-lookup"><span data-stu-id="23943-136">Yes</span></span> | <span data-ttu-id="23943-137">Sì</span><span class="sxs-lookup"><span data-stu-id="23943-137">Yes</span></span> |
| <span data-ttu-id="23943-138">Modificare i metadati dell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="23943-138">Change organization metadata</span></span><br/><span data-ttu-id="23943-139">(indirizzi di posta elettronica, impostazioni di notifica)</span><span class="sxs-lookup"><span data-stu-id="23943-139">(email address, notification settings)</span></span> | <span data-ttu-id="23943-140">No</span><span class="sxs-lookup"><span data-stu-id="23943-140">No</span></span> | <span data-ttu-id="23943-141">Sì</span><span class="sxs-lookup"><span data-stu-id="23943-141">Yes</span></span> |
| <span data-ttu-id="23943-142">Gestire i membri dell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="23943-142">Manage organization members</span></span> | <span data-ttu-id="23943-143">No</span><span class="sxs-lookup"><span data-stu-id="23943-143">No</span></span> | <span data-ttu-id="23943-144">Sì</span><span class="sxs-lookup"><span data-stu-id="23943-144">Yes</span></span> |
| <span data-ttu-id="23943-145">Richiedere o gestire richieste di comproprietà per pacchetti dell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="23943-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="23943-146">No</span><span class="sxs-lookup"><span data-stu-id="23943-146">No</span></span> | <span data-ttu-id="23943-147">Sì</span><span class="sxs-lookup"><span data-stu-id="23943-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="23943-148">Gestione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="23943-148">Managing packages</span></span>

<span data-ttu-id="23943-149">È possibile visualizzare tutti i pacchetti dell'account e di tutte le organizzazioni di cui si è membro nella pagina [Manage Packages](https://www.nuget.org/account/Packages) (Gestisci pacchetti).</span><span class="sxs-lookup"><span data-stu-id="23943-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="23943-150">Per visualizzare i pacchetti specifici dell'account o di una qualsiasi organizzazione, usare il filtro di account nella parte superiore destra della pagina.</span><span class="sxs-lookup"><span data-stu-id="23943-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Gestione di pacchetti con il filtro di account](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="23943-152">Trasferimento di pacchetti a un'organizzazione</span><span class="sxs-lookup"><span data-stu-id="23943-152">Transferring packages to an organization</span></span>
<span data-ttu-id="23943-153">Se si vogliono trasferire alcuni pacchetti a un'organizzazione appena creata, è necessario richiedere l'account aziendale per diventare comproprietari del pacchetto e rimuovere se stesso come proprietario.</span><span class="sxs-lookup"><span data-stu-id="23943-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="23943-154">Se si è amministratore dell'organizzazione, non è necessaria una conferma di accettazione della proprietà.</span><span class="sxs-lookup"><span data-stu-id="23943-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="23943-155">Se si è invece collaboratore, per poter aggiungere l'organizzazione come proprietario è necessario che uno degli amministratori accetti la proprietà.</span><span class="sxs-lookup"><span data-stu-id="23943-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="23943-156">Pubblicazione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="23943-156">Publishing packages</span></span>

<span data-ttu-id="23943-157">I pacchetti vengono pubblicati in un'organizzazione esattamente con in un account utente. È possibile caricare il pacchetto direttamente in NuGet.org oppure pubblicarlo tramite i comandi dell'interfaccia della riga di comando `nuget push` o `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="23943-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to NuGet.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="23943-158">Caricamento di pacchetti</span><span class="sxs-lookup"><span data-stu-id="23943-158">Uploading packages</span></span>

<span data-ttu-id="23943-159">Quando si carica direttamente un nuovo pacchetto nella pagina [Upload](https://www.nuget.org/packages/manage/upload) (Carica ) di NuGet.org, si assegna il proprietario del pacchetto a un account utente o aziendale:</span><span class="sxs-lookup"><span data-stu-id="23943-159">When you directly upload a new package on the [NuGet.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Caricare un pacchetto con l'opzione account](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="23943-161">Uso di chiavi API</span><span class="sxs-lookup"><span data-stu-id="23943-161">Using API keys</span></span>

<span data-ttu-id="23943-162">Per eseguire il push di un pacchetto tramite i comandi dell'interfaccia della riga di comando `nuget push` o `dotnet nuget push`, è necessario ottenere una chiave API richiesta da tali comandi.</span><span class="sxs-lookup"><span data-stu-id="23943-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="23943-163">Per informazioni dettagliate, vedere [Pubblicare un pacchetto](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="23943-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="23943-164">Quando si crea una nuova chiave API, selezionare l'organizzazione appropriata nell'elenco a discesa **Package Owner** (Proprietario pacchetto).</span><span class="sxs-lookup"><span data-stu-id="23943-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="23943-165">Le chiavi API create sono applicabili solo all'organizzazione selezionata:</span><span class="sxs-lookup"><span data-stu-id="23943-165">Any API key you create is applicable only to the chosen organization:</span></span>

![Chiave API con opzione account](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="23943-167">Uscita da un'organizzazione</span><span class="sxs-lookup"><span data-stu-id="23943-167">Removing an organization</span></span>

<span data-ttu-id="23943-168">Un utente può uscire da un'organizzazione selezionando il pulsante **X** visualizzato dall'appartenenza all'organizzazione:</span><span class="sxs-lookup"><span data-stu-id="23943-168">As a user, you can remove yourself from an organization by selecting the **X** button shown by your organization membership:</span></span>

![Rimozione di un account utente da un'organizzazione](media/org-remove-self-option.png)

<span data-ttu-id="23943-170">Gli amministratori possono rimuovere tutti i membri dell'organizzazione, inclusi altri amministratori.</span><span class="sxs-lookup"><span data-stu-id="23943-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="23943-171">Se si è il solo amministratore di un'organizzazione, non è possibile rimuovere se stessi a meno che non si aggiunga un altro membro come amministratore.</span><span class="sxs-lookup"><span data-stu-id="23943-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="23943-172">Eliminazione di un account aziendale</span><span class="sxs-lookup"><span data-stu-id="23943-172">Deleting an organization account</span></span>

<span data-ttu-id="23943-173">È possibile eliminare un account aziendale facendo clic sul pulsante **Delete** (Elimina) visualizzato nella pagina dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="23943-173">You can delete an organization account by clicking the **Delete** button shown in your organization page.</span></span>

![Eliminazione di un'organizzazione](media/org-delete-option.png)

<span data-ttu-id="23943-175">Per eliminare l'organizzazione, confermare l'operazione facendo clic sul pulsante di conferma **Delete organization** (Elimina organizzazione).</span><span class="sxs-lookup"><span data-stu-id="23943-175">To delete the organizaiton, you must confirm it by clicking the **Delete organization** confirmation button.</span></span>
