---
title: Come pubblicare un pacchetto NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Istruzioni dettagliate su come pubblicare un pacchetto NuGet in nuget.org o in feed privati e su come gestire la proprietà del pacchetto in nuget.org.
keywords: pubblicazione di un pacchetto NuGet, pubblicare un pacchetto NuGet, proprietà del pacchetto NuGet, pubblicare in nuget.org, feed NuGet privati
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 68db25276297353fab03258adecd9169149dbe51
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="publishing-packages"></a><span data-ttu-id="d4aef-104">Pubblicazione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="d4aef-104">Publishing packages</span></span>

<span data-ttu-id="d4aef-105">Dopo avere creato un pacchetto e con il file `.nukpg` a portata di mano, il processo per renderlo disponibile per altri sviluppatori, pubblicamente o privatamente, è davvero semplice:</span><span class="sxs-lookup"><span data-stu-id="d4aef-105">Once you have created a package and have your `.nukpg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="d4aef-106">I pacchetti pubblici diventano disponibili per tutti gli sviluppatori a livello globale tramite [nuget.org](https://www.nuget.org/packages/manage/upload), come descritto in questo articolo (è richiesto NuGet 4.1.0+).</span><span class="sxs-lookup"><span data-stu-id="d4aef-106">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this article (requires NuGet 4.1.0+).</span></span>
- <span data-ttu-id="d4aef-107">I pacchetti privati, disponibili solo per un team o un'organizzazione, sono ospitati in una condivisione file, in un server NuGet privato, in [Gestione pacchetti di Visual Studio Team Services](https://www.visualstudio.com/docs/package/nuget/publish) o in un repository di terze parti, ad esempio myget, ProGet, Nexus Repository e Artifactory.</span><span class="sxs-lookup"><span data-stu-id="d4aef-107">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="d4aef-108">Per altre informazioni, vedere [Panoramica dell'hosting dei pacchetti](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="d4aef-108">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="d4aef-109">Questo articolo illustra la pubblicazione in nuget.org. Per la pubblicazione in Visual Studio Team Services, vedere [Package Management](https://www.visualstudio.com/docs/package/nuget/publish) (Gestione pacchetti).</span><span class="sxs-lookup"><span data-stu-id="d4aef-109">This article covers publishing to nuget.org; for publishing to Visual Studio Team Services, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="d4aef-110">Pubblicare in nuget.org</span><span class="sxs-lookup"><span data-stu-id="d4aef-110">Publish to nuget.org</span></span>

<span data-ttu-id="d4aef-111">Per nuget.org è necessario accedere con un account Microsoft, con il quale verrà richiesto di registrare l'account in nuget.org. È anche possibile accedere con un account di nuget.org creato con le versioni precedenti del portale.</span><span class="sxs-lookup"><span data-stu-id="d4aef-111">For nuget.org, you must sign in with a Microsoft account, with which you'll be asked to register the account with nuget.org. You can also sign in with a nuget.org account created using older versions of the portal.</span></span>

![Posizione di accesso a NuGet](media/publish_NuGetSignIn.png)

<span data-ttu-id="d4aef-113">Sarà quindi possibile caricare il pacchetto tramite il portale Web di nuget.org, eseguire il push in nuget.org dalla riga di comando (è richiesto `nuget.exe` 4.1.0+) o effettuare la pubblicazione durante un processo di integrazione continua/recapito continuo tramite Visual Studio Team Services, come descritto nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="d4aef-113">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Visual Studio Team Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="d4aef-114">Portale Web: usare la scheda Upload Package (Carica pacchetto) in nuget.org</span><span class="sxs-lookup"><span data-stu-id="d4aef-114">Web portal: use the Upload Package tab on nuget.org</span></span>

1. <span data-ttu-id="d4aef-115">Selezionare **Upload**  (Carica) nel menu in alto di nuget.org e passare alla posizione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d4aef-115">Select **Upload** on the top menu of nuget.org and browse to the package location.</span></span>

    ![Caricare un pacchetto in nuget.org](media/publish_UploadYourPackage.PNG)

1. <span data-ttu-id="d4aef-117">Nuget.org indica se il nome del pacchetto è disponibile.</span><span class="sxs-lookup"><span data-stu-id="d4aef-117">nuget.org tells you if the package name is available.</span></span> <span data-ttu-id="d4aef-118">Se non lo è, modificare l'identificatore del pacchetto nel progetto, ricompilare e riprovare a eseguire il caricamento.</span><span class="sxs-lookup"><span data-stu-id="d4aef-118">If it isn't, change the package identifier in your project, rebuild, and try the upload again.</span></span>

1. <span data-ttu-id="d4aef-119">Se il nome del pacchetto è disponibile, nuget.org apre una sezione **Verify** (Verifica) in cui è possibile esaminare i metadati del manifesto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d4aef-119">If the package name is available, nuget.org opens a **Verify** section in which you can review the metadata from the package manifest.</span></span> <span data-ttu-id="d4aef-120">Per modificare i metadati, modificare il progetto (file di progetto o file `.nuspec`), ricompilare, ricreare il pacchetto e caricarlo nuovamente.</span><span class="sxs-lookup"><span data-stu-id="d4aef-120">To change any of the metadata, edit your project (project file or `.nuspec` file), rebuild, recreate the package, and upload again.</span></span>

1. <span data-ttu-id="d4aef-121">In **Import Documentation** (Importa documentazione) è possibile incollare Markdown, selezionare documenti con un URL oppure caricare un file di documentazione.</span><span class="sxs-lookup"><span data-stu-id="d4aef-121">Under **Import Documentation** you can paste Markdown, point to your docs with a URL, or upload a documentation file.</span></span>

1. <span data-ttu-id="d4aef-122">Quando tutte le informazioni sono pronte, selezionare il pulsante **Submit** (Invia).</span><span class="sxs-lookup"><span data-stu-id="d4aef-122">When all the information is ready, select the **Submit** button</span></span>

### <a name="command-line"></a><span data-ttu-id="d4aef-123">Riga di comando</span><span class="sxs-lookup"><span data-stu-id="d4aef-123">Command line</span></span>

<span data-ttu-id="d4aef-124">Per eseguire il push dei pacchetti in nuget.org, è necessario usare [nuget.exe v4.1.0 o versione successiva](https://www.nuget.org/downloads), che implementa i [protocolli NuGet](../api/nuget-protocols.md) necessari.</span><span class="sxs-lookup"><span data-stu-id="d4aef-124">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span> <span data-ttu-id="d4aef-125">È anche necessaria una chiave API, che viene creata in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d4aef-125">You also need an API key, which is created on nuget.org.</span></span>

#### <a name="create-api-keys"></a><span data-ttu-id="d4aef-126">Creare chiavi API</span><span class="sxs-lookup"><span data-stu-id="d4aef-126">Create API keys</span></span>

[!INCLUDE[publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="d4aef-127">Pubblicare con dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="d4aef-127">Publish with dotnet nuget push</span></span>

[!INCLUDE[publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a><span data-ttu-id="d4aef-128">Pubblicare con nuget push</span><span class="sxs-lookup"><span data-stu-id="d4aef-128">Publish with nuget push</span></span>

1. <span data-ttu-id="d4aef-129">Al prompt dei comandi, eseguire il comando seguente, sostituendo `<your_API_key>` con la chiave ottenuta da nuget.org:</span><span class="sxs-lookup"><span data-stu-id="d4aef-129">At a command prompt, run the following command, replacing `<your_API_key>` with the key obtained from nuget.org:</span></span>

    ```cli
    nuget setApiKey <your_API_key>
    ```

    <span data-ttu-id="d4aef-130">Questo comando archivia la chiave API nella configurazione NuGet in modo che non sia necessario ripetere questo passaggio nuovamente nello stesso computer.</span><span class="sxs-lookup"><span data-stu-id="d4aef-130">This command stores your API key in your NuGet configuration so that you need repeat this step again on the same computer.</span></span>

1. <span data-ttu-id="d4aef-131">Eseguire il push del pacchetto nella raccolta NuGet usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d4aef-131">Push your package to NuGet Gallery using the following command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

### <a name="package-validation-and-indexing"></a><span data-ttu-id="d4aef-132">Convalida e indicizzazione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="d4aef-132">Package validation and indexing</span></span>

<span data-ttu-id="d4aef-133">I pacchetti di cui viene eseguito il push in nuget.org vengono sottoposti a diverse convalide, ad esempio il controllo antivirus.</span><span class="sxs-lookup"><span data-stu-id="d4aef-133">Packages pushed to nuget.org undergo several validations, such as virus checks.</span></span> <span data-ttu-id="d4aef-134">(Tutti i pacchetti in nuget.org vengono analizzati periodicamente.)</span><span class="sxs-lookup"><span data-stu-id="d4aef-134">(All packages on nuget.org are periodically scanned.)</span></span>

<span data-ttu-id="d4aef-135">.</span><span class="sxs-lookup"><span data-stu-id="d4aef-135">.</span></span> <span data-ttu-id="d4aef-136">Quando il pacchetto ha superato tutti i controlli di convalida, l'indicizzazione e la visualizzazione del pacchetto nei risultati della ricerca potrebbero richiedere qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="d4aef-136">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="d4aef-137">Al termine dell'indicizzazione, viene visualizzato un messaggio di posta elettronica che conferma che il pacchetto è stato pubblicato.</span><span class="sxs-lookup"><span data-stu-id="d4aef-137">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="d4aef-138">Se il pacchetto non supera un controllo di convalida, la pagina dei dettagli del pacchetto verrà aggiornata con l'errore associato e si riceverà anche una notifica tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="d4aef-138">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="d4aef-139">La convalida e l'indicizzazione del pacchetto richiedono in genere meno di 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="d4aef-139">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="d4aef-140">Se la pubblicazione del pacchetto richiede più tempo del previsto, visitare [status.nuget.org](https://status.nuget.org/) per controllare se si stanno verificando interruzioni in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d4aef-140">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="d4aef-141">Se tutti i sistemi sono operativi e il pacchetto non viene pubblicato entro un'ora, accedere a nuget.org e usare il collegamento per contattare il supporto tecnico nella pagina del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d4aef-141">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

<span data-ttu-id="d4aef-142">Per visualizzare lo stato di un pacchetto, selezionare **Manage packages** (Gestisci pacchetti) sotto il nome di account in nuget.org. Al termine della convalida si riceverà un messaggio di posta elettronica di conferma.</span><span class="sxs-lookup"><span data-stu-id="d4aef-142">To see the status of a package, select **Manage packages** under your account name on nuget.org. You receive a confirmation email when validation is complete.</span></span>

<span data-ttu-id="d4aef-143">Si noti che l'indicizzazione e la visualizzazione del pacchetto nei risultati della ricerca, dove altri possono trovarlo, potrebbero richiedere tempo. Nella pagina del pacchetto viene nel frattempo visualizzato il messaggio seguente:</span><span class="sxs-lookup"><span data-stu-id="d4aef-143">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

![Messaggio indicante che un pacchetto non è ancora stato pubblicato](media/publish_NotYetIndexed.png)

### <a name="visual-studio-team-services-cicd"></a><span data-ttu-id="d4aef-145">Visual Studio Team Services (integrazione continua/recapito continuo)</span><span class="sxs-lookup"><span data-stu-id="d4aef-145">Visual Studio Team Services (CI/CD)</span></span>

<span data-ttu-id="d4aef-146">Se si esegue il push dei pacchetti in nuget.org usando Visual Studio Team Services durante il processo di integrazione continua/recapito continuo, è necessario usare `nuget.exe` 4.1 o versione successiva nelle attività NuGet.</span><span class="sxs-lookup"><span data-stu-id="d4aef-146">If you push packages to nuget.org using Visual Studio Team Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="d4aef-147">Per informazioni, vedere [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Uso della versione più recente di NuGet nella compilazione) nel blog di Microsoft DevOps.</span><span class="sxs-lookup"><span data-stu-id="d4aef-147">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="d4aef-148">Gestione dei proprietari dei pacchetti in nuget.org</span><span class="sxs-lookup"><span data-stu-id="d4aef-148">Managing package owners on nuget.org</span></span>

<span data-ttu-id="d4aef-149">Anche se ogni file `.nuspec` del pacchetto NuGet definisce gli autori del pacchetto, la raccolta nuget.org non usa tali metadati per definire la proprietà.</span><span class="sxs-lookup"><span data-stu-id="d4aef-149">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="d4aef-150">Nuget.org assegna invece la proprietà iniziale alla persona che pubblica il pacchetto,</span><span class="sxs-lookup"><span data-stu-id="d4aef-150">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="d4aef-151">ovvero l'utente connesso che ha caricato il pacchetto tramite l'interfaccia utente di nuget.org o gli utenti la cui chiave API è stata usata con `nuget SetApiKey` o `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="d4aef-151">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="d4aef-152">Tutti i proprietari del pacchetto hanno autorizzazioni complete per il pacchetto, incluse l'aggiunta e la rimozione di altri proprietari e la pubblicazione di aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="d4aef-152">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="d4aef-153">Per modificare il proprietario di un pacchetto, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d4aef-153">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="d4aef-154">Accedere a nuget.org con l'account che è il proprietario corrente del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d4aef-154">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="d4aef-155">Selezionare il nome dell'account, selezionare **Manage packages** (Gestisci pacchetti) ed espandere **Published Packages** (Pacchetti pubblicati).</span><span class="sxs-lookup"><span data-stu-id="d4aef-155">Select your account name, select **Manage packages**, and expand **Published Packages**.</span></span>
1. <span data-ttu-id="d4aef-156">Selezionare il pacchetto che si vuole gestire e quindi sul lato destro selezionare **Manage owners** (Gestisci proprietari).</span><span class="sxs-lookup"><span data-stu-id="d4aef-156">Select on the package you want to manage, then on the right side select **Manage owners**.</span></span>

<span data-ttu-id="d4aef-157">A questo punto sono disponibili diverse alternative:</span><span class="sxs-lookup"><span data-stu-id="d4aef-157">From here you have several options:</span></span>

1. <span data-ttu-id="d4aef-158">Rimuovere qualsiasi proprietario elencato in **Current Owners** (Proprietari correnti).</span><span class="sxs-lookup"><span data-stu-id="d4aef-158">Remove any owner listed under **Current Owners**.</span></span>
1. <span data-ttu-id="d4aef-159">Aggiungere un proprietario in **Add Owner** (Aggiungi proprietario) immettendo il nome utente, un messaggio e selezionando **Add** (Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="d4aef-159">Add an owner under **Add Owner** by entering their user name, a message, and selecting **Add**.</span></span> <span data-ttu-id="d4aef-160">Questa azione invia a tale nuovo comproprietario un messaggio di posta elettronica con un collegamento di conferma.</span><span class="sxs-lookup"><span data-stu-id="d4aef-160">This action sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="d4aef-161">Dopo la conferma, tale persona ha le autorizzazioni complete per aggiungere e rimuovere i proprietari.</span><span class="sxs-lookup"><span data-stu-id="d4aef-161">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="d4aef-162">Fino all'avvenuta conferma, la sezione **Current Owners** (Proprietari correnti) indica l'approvazione in sospeso per tale persona.</span><span class="sxs-lookup"><span data-stu-id="d4aef-162">(Until confirmed, the **Current Owners** section indicates pending approval for that person.)</span></span>
1. <span data-ttu-id="d4aef-163">Per trasferire la proprietà (ad esempio quando la proprietà cambia o un pacchetto è stato pubblicato con l'account errato), aggiungere il nuovo proprietario che, dopo avere confermato la proprietà, potrà rimuovere l'utente dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="d4aef-163">To transfer ownership (as when ownership changes or a package was published under the wrong account), add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="d4aef-164">Per assegnare la proprietà a una società o a un gruppo, creare un account nuget.org usando un alias di posta elettronica che viene inoltrato ai membri del team appropriati.</span><span class="sxs-lookup"><span data-stu-id="d4aef-164">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="d4aef-165">Diversi pacchetti Microsoft ASP.NET, ad esempio, sono in comproprietà con gli account [microsoft](http://nuget.org/profiles/microsoft) e [aspnet](http://nuget.org/profiles/aspnet) e tali alias risultano semplificati.</span><span class="sxs-lookup"><span data-stu-id="d4aef-165">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="d4aef-166">Ripristino della proprietà di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="d4aef-166">Recovering package ownership</span></span>

<span data-ttu-id="d4aef-167">Può capitare che un pacchetto non abbia un proprietario attivo.</span><span class="sxs-lookup"><span data-stu-id="d4aef-167">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="d4aef-168">È ad esempio possibile che il proprietario originale abbia lasciato la società che produce il pacchetto, che le credenziali nuget.org vadano perse o che bug precedenti nella raccolta abbiano lasciato un pacchetto senza proprietario.</span><span class="sxs-lookup"><span data-stu-id="d4aef-168">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="d4aef-169">Se il proprietario legittimo di un pacchetto ha la necessità di ripristinare la proprietà, deve usare il [modulo contatto](https://www.nuget.org/policies/Contact) su nuget.org per illustrare la situazione al team di NuGet.</span><span class="sxs-lookup"><span data-stu-id="d4aef-169">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="d4aef-170">Viene quindi messo in atto un processo per verificare la proprietà del pacchetto, che include il tentativo di rintracciare il proprietario esistente tramite l'URL del progetto del pacchetto, Twitter, posta elettronica o altri mezzi.</span><span class="sxs-lookup"><span data-stu-id="d4aef-170">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="d4aef-171">Se ogni tentativo ha esito negativo, è possibile inviare all'utente un nuovo invito a diventare proprietario.</span><span class="sxs-lookup"><span data-stu-id="d4aef-171">But if all else fails, we can send you a new invite to become an owner.</span></span>
