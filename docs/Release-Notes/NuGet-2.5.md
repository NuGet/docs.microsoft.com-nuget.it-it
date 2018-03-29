---
title: Note sulla versione di NuGet 2.5 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Note sulla versione per NuGet 2.5 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
keywords: NuGet 2.5 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4495e1ea9cc4ec13ef330e56d12de1320cf10b24
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="f8681-104">Note sulla versione 2.5 di NuGet</span><span class="sxs-lookup"><span data-stu-id="f8681-104">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="f8681-105">[Note sulla versione 2.2.1 NuGet](../release-notes/nuget-2.2.1.md) | [note sulla versione 2.6 NuGet](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="f8681-105">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="f8681-106">NuGet 2.5 è stata rilasciata il 25 aprile 2013.</span><span class="sxs-lookup"><span data-stu-id="f8681-106">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="f8681-107">Questa versione è stata così grande, è stato ritenuto obbligati a ignorare versioni 2.3 e 2.4.</span><span class="sxs-lookup"><span data-stu-id="f8681-107">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="f8681-108">Per data, questa è la versione più grande, abbiamo utilizzato per NuGet, con su [gli elementi di lavoro di 160](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) nella versione.</span><span class="sxs-lookup"><span data-stu-id="f8681-108">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="f8681-109">Riconoscimenti</span><span class="sxs-lookup"><span data-stu-id="f8681-109">Acknowledgements</span></span>

<span data-ttu-id="f8681-110">Si ringraziano i collaboratori esterni seguenti per il loro contributo significativo a NuGet 2.5:</span><span class="sxs-lookup"><span data-stu-id="f8681-110">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="f8681-111">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="f8681-111">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="f8681-112">[#2847](https://nuget.codeplex.com/workitem/2847) -aggiungere MonoAndroid MonoTouch e MonoMac all'elenco di identificatori di framework di destinazione noti.</span><span class="sxs-lookup"><span data-stu-id="f8681-112">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
1. <span data-ttu-id="f8681-113">[Aragoneses g. Andres](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="f8681-113">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="f8681-114">[#2865](https://nuget.codeplex.com/workitem/2865) -correggere l'ortografia del `NuGet.targets` per un sistema operativo di distinzione maiuscole/minuscole</span><span class="sxs-lookup"><span data-stu-id="f8681-114">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
1. <span data-ttu-id="f8681-115">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="f8681-115">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="f8681-116">Rendere la soluzione di compilazione su Mono.</span><span class="sxs-lookup"><span data-stu-id="f8681-116">Make the solution build on Mono.</span></span>
1. <span data-ttu-id="f8681-117">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="f8681-117">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="f8681-118">Correggere gli unit test non superati in Mono.</span><span class="sxs-lookup"><span data-stu-id="f8681-118">Fix unit tests failing on Mono.</span></span>
1. <span data-ttu-id="f8681-119">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="f8681-119">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="f8681-120">[#2920](https://nuget.codeplex.com/workitem/2920) -comando di nuget.exe pack non propaga le proprietà di MSBuild</span><span class="sxs-lookup"><span data-stu-id="f8681-120">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
1. <span data-ttu-id="f8681-121">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="f8681-121">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="f8681-122">[#1511](https://nuget.codeplex.com/workitem/1511) - XML modificato la gestione del codice per mantenere la formattazione.</span><span class="sxs-lookup"><span data-stu-id="f8681-122">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
1. <span data-ttu-id="f8681-123">[ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="f8681-123">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="f8681-124">Riconosciuta per parole aggiunte al dizionario personalizzato per consentire build.cmd abbia esito positivo.</span><span class="sxs-lookup"><span data-stu-id="f8681-124">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
1. [<span data-ttu-id="f8681-125">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="f8681-125">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="f8681-126">Correggere gli unit test durante l'esecuzione in Visual Studio localizzata.</span><span class="sxs-lookup"><span data-stu-id="f8681-126">Fix unit tests when running in localized VS.</span></span>
1. [<span data-ttu-id="f8681-127">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="f8681-127">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="f8681-128">Interfaccia estratto da PackageService</span><span class="sxs-lookup"><span data-stu-id="f8681-128">Extracted interface from PackageService</span></span>
1. <span data-ttu-id="f8681-129">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="f8681-129">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
    - <span data-ttu-id="f8681-130">[#936](https://nuget.codeplex.com/workitem/936) -gestire le dipendenze di progetto quando compressione</span><span class="sxs-lookup"><span data-stu-id="f8681-130">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
1. <span data-ttu-id="f8681-131">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="f8681-131">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
    - <span data-ttu-id="f8681-132">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -supporto Password come testo non crittografato quando si archiviano le credenziali dell'origine del pacchetto nel file nuget.cofig</span><span class="sxs-lookup"><span data-stu-id="f8681-132">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
1. <span data-ttu-id="f8681-133">[Supervisione relativo personale James](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="f8681-133">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
    - <span data-ttu-id="f8681-134">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -descrizione della Guida correggere Get-Package</span><span class="sxs-lookup"><span data-stu-id="f8681-134">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="f8681-135">Si apprezza anche gli utenti seguenti per la ricerca di bug con NuGet 2.5 Beta o RC che sono stati approvati e risolto prima della versione finale:</span><span class="sxs-lookup"><span data-stu-id="f8681-135">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="f8681-136">[Tony parete](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="f8681-136">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="f8681-137">[#3200](https://nuget.codeplex.com/workitem/3200) MSTest interrotto con più di recente NuGet 2.4 e 2.5 compilazioni:</span><span class="sxs-lookup"><span data-stu-id="f8681-137">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="f8681-138">Importanti funzionalità nella versione</span><span class="sxs-lookup"><span data-stu-id="f8681-138">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="f8681-139">Consentire agli utenti di sovrascrivere i file di contenuto che esistono già</span><span class="sxs-lookup"><span data-stu-id="f8681-139">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="f8681-140">Una delle funzionalità più richieste di tutto il tempo è stata la possibilità di sovrascrivere i file di contenuto che già esistono nel disco quando incluso in un pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="f8681-140">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="f8681-141">A partire da NuGet 2.5, tali conflitti vengono identificati e viene chiesto di sovrascrivere i file, mentre in precedenza sempre ignorati questi file.</span><span class="sxs-lookup"><span data-stu-id="f8681-141">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Sovrascrivere i file di contenuto](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="f8681-143">'nuget.exe update' e 'Install-Package' ora dispongono di una nuova opzione '-FileConflictAction' per impostare alcuni valori predefiniti per gli scenari della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="f8681-143">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="f8681-144">Impostare un'azione predefinita quando un file da un pacchetto esiste già nel progetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="f8681-144">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="f8681-145">Impostare su 'Sovrascrivi' per sovrascrivere sempre i file.</span><span class="sxs-lookup"><span data-stu-id="f8681-145">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="f8681-146">Impostare su 'Ignora' per ignorare i file.</span><span class="sxs-lookup"><span data-stu-id="f8681-146">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="f8681-147">Se non specificato, verrà richiesto per ogni file in conflitto.</span><span class="sxs-lookup"><span data-stu-id="f8681-147">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="f8681-148">Importazione automatica dei file props e destinazioni di MSBuild</span><span class="sxs-lookup"><span data-stu-id="f8681-148">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="f8681-149">Una nuova cartella convenzionale è stata creata al primo livello del pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="f8681-149">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="f8681-150">Allo stesso livello `\lib`, `\content`, e `\tools`, ora è possibile includere un `\build` cartella nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f8681-150">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="f8681-151">In questa cartella, è possibile inserire due file con nomi fissi, `{packageid}.targets` o `{packageid}.props`.</span><span class="sxs-lookup"><span data-stu-id="f8681-151">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="f8681-152">Questi due file possono essere direttamente in `build` o in cartelle specifiche del framework come le altre cartelle.</span><span class="sxs-lookup"><span data-stu-id="f8681-152">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="f8681-153">La regola per scegliere la cartella di .NET framework corrispondente con mapping più appropriato è esattamente uguale a quello di quelli.</span><span class="sxs-lookup"><span data-stu-id="f8681-153">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="f8681-154">Quando si NuGet installa un pacchetto con file \build, aggiungerà un MSBuild `<Import>` nel file di progetto che punta all'elemento di `.targets` e `.props` file.</span><span class="sxs-lookup"><span data-stu-id="f8681-154">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="f8681-155">Il `.props` file viene aggiunto all'inizio, mentre il `.targets` file viene aggiunto alla fine.</span><span class="sxs-lookup"><span data-stu-id="f8681-155">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="f8681-156">Specificare i riferimenti diversi per ogni piattaforma utilizzando `<References/>` elemento</span><span class="sxs-lookup"><span data-stu-id="f8681-156">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="f8681-157">Prima di 2.5 in `.nuspec` file utente può specificare solo i file di riferimento da aggiungere per tutti i framework.</span><span class="sxs-lookup"><span data-stu-id="f8681-157">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="f8681-158">Ora con questa nuova funzionalità in 2.5, è possibile creare l'utente di `<reference/>` elemento per ogni piattaforma supportata, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="f8681-158">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

<span data-ttu-id="f8681-159">Di seguito viene illustrato il flusso per la modalità NuGet aggiunge riferimenti ai progetti basati sul `.nuspec` file:</span><span class="sxs-lookup"><span data-stu-id="f8681-159">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="f8681-160">Trovare il `lib` cartella appropriata per il framework di destinazione e ottiene l'elenco degli assembly dalla cartella</span><span class="sxs-lookup"><span data-stu-id="f8681-160">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="f8681-161">Separatamente, trovare il gruppo di riferimenti che è appropriato per il framework di destinazione e ottenere l'elenco degli assembly da quel gruppo.</span><span class="sxs-lookup"><span data-stu-id="f8681-161">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="f8681-162">Gruppo di riferimenti senza il framework di destinazione specificato è il gruppo di fallback.</span><span class="sxs-lookup"><span data-stu-id="f8681-162">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="f8681-163">Trovare l'intersezione dei due elenchi e utilizzarlo come i riferimenti da aggiungere</span><span class="sxs-lookup"><span data-stu-id="f8681-163">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="f8681-164">Questa nuova funzionalità consente agli autori di pacchetti di utilizzare la funzionalità di riferimenti ad per applicare subset di assembly Framework diversi quando sono sarebbe altrimenti necessario per eseguire gli assembly duplicati in più `lib` cartelle.</span><span class="sxs-lookup"><span data-stu-id="f8681-164">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="f8681-165">Nota: al momento utilizzare nuget.exe pack per utilizzare questa funzionalità; Esplora pacchetti NuGet non supporta ancora il.</span><span class="sxs-lookup"><span data-stu-id="f8681-165">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="f8681-166">Aggiornare tutti i pulsante per consentire l'aggiornamento di tutti i pacchetti in una sola volta</span><span class="sxs-lookup"><span data-stu-id="f8681-166">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="f8681-167">Molti di voi conoscere il cmdlet PowerShell di "Pacchetto di aggiornamento" per aggiornare tutti i pacchetti; è ora un modo semplice per eseguire questa operazione tramite l'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="f8681-167">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="f8681-168">Per provare questa funzionalità:</span><span class="sxs-lookup"><span data-stu-id="f8681-168">To try this feature out:</span></span>

1. <span data-ttu-id="f8681-169">Creare una nuova applicazione MVC ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f8681-169">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="f8681-170">Avviare la finestra di dialogo 'Gestisci pacchetti di NuGet'</span><span class="sxs-lookup"><span data-stu-id="f8681-170">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="f8681-171">Selezionare 'Updates'</span><span class="sxs-lookup"><span data-stu-id="f8681-171">Select 'Updates'</span></span>
1. <span data-ttu-id="f8681-172">Fare clic sul pulsante 'Aggiorna tutto'</span><span class="sxs-lookup"><span data-stu-id="f8681-172">Click the 'Update All' button</span></span>

![Aggiornare tutti i pulsante nella finestra di dialogo](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="f8681-174">Supporto di riferimento di progetto migliorato per nuget.exe Pack</span><span class="sxs-lookup"><span data-stu-id="f8681-174">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="f8681-175">A questo punto i processi di comando di nuget.exe pack riferimento progetti con le regole seguenti:</span><span class="sxs-lookup"><span data-stu-id="f8681-175">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="f8681-176">Se il progetto di riferimento corrispondente `.nuspec` file, ad esempio, è presente un file denominato `proj1.nuspec` nella stessa cartella `proj1.csproj`, quindi questo progetto viene aggiunto come una dipendenza per il pacchetto, utilizzando l'id e versione sono leggervi il `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="f8681-176">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="f8681-177">In caso contrario, i file del progetto di riferimento sono inclusi nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f8681-177">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="f8681-178">Quindi verranno elaborati i progetti a cui fa riferimento questo progetto utilizzando le regole di medesime in modo ricorsivo.</span><span class="sxs-lookup"><span data-stu-id="f8681-178">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="f8681-179">Tutte le DLL, `.pdb`, e `.exe` file vengono aggiunti.</span><span class="sxs-lookup"><span data-stu-id="f8681-179">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="f8681-180">Tutti gli altri file di contenuto vengono aggiunti.</span><span class="sxs-lookup"><span data-stu-id="f8681-180">All other content files are added.</span></span>
1. <span data-ttu-id="f8681-181">Tutte le dipendenze vengono unite.</span><span class="sxs-lookup"><span data-stu-id="f8681-181">All dependencies are merged.</span></span>

<span data-ttu-id="f8681-182">In questo modo un progetto di riferimento devono essere considerati una dipendenza, se è presente un `.nuspec` file, in caso contrario, diventa parte del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f8681-182">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="f8681-183">Ulteriori dettagli di seguito: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="f8681-183">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="f8681-184">Aggiungere una proprietà 'La versione minima NuGet' per i pacchetti</span><span class="sxs-lookup"><span data-stu-id="f8681-184">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="f8681-185">Un nuovo attributo di metadati denominato 'minClientVersion' ora può indicare la versione minima del client NuGet necessaria per utilizzare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f8681-185">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="f8681-186">Questa funzionalità consente l'autore del pacchetto per specificare che un pacchetto funzionerà solo dopo una particolare versione di NuGet.</span><span class="sxs-lookup"><span data-stu-id="f8681-186">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="f8681-187">Come nuovi `.nuspec` dopo NuGet 2.5, sono state aggiunte funzionalità pacchetti saranno in grado di richiedere una versione minima di NuGet.</span><span class="sxs-lookup"><span data-stu-id="f8681-187">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="f8681-188">Se l'utente abbia NuGet 2.5 installato e un pacchetto è stato identificato come richiedere 2.6, segnali visivi verranno forniti all'utente che indica che il pacchetto non sarà installabile.</span><span class="sxs-lookup"><span data-stu-id="f8681-188">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="f8681-189">L'utente verrà quindi essere guidata per l'aggiornamento della versione di NuGet.</span><span class="sxs-lookup"><span data-stu-id="f8681-189">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="f8681-190">Questo verrà migliorano l'esperienza esistente in cui iniziano i pacchetti da installare, ma prima dell'esito negativo che indica che è stata identificata una versione dello schema non riconosciuto.</span><span class="sxs-lookup"><span data-stu-id="f8681-190">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="f8681-191">Le dipendenze non è più inutilmente vengono aggiornate durante l'installazione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="f8681-191">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="f8681-192">Prima di NuGet 2.5, durante l'installazione di un pacchetto che dipendono da un pacchetto già installato nel progetto, la dipendenza verranno aggiornata come parte della nuova installazione, anche se la versione esistente è soddisfatta la dipendenza.</span><span class="sxs-lookup"><span data-stu-id="f8681-192">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="f8681-193">A partire da NuGet 2.5, se una versione della dipendenza già viene soddisfatta, la dipendenza non verrà aggiornata durante le altre installazioni del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f8681-193">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="f8681-194">**Scenario:**</span><span class="sxs-lookup"><span data-stu-id="f8681-194">**The scenario:**</span></span>

1. <span data-ttu-id="f8681-195">Il repository di origine contiene pacchetto B con la versione 1.0.0 e 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="f8681-195">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="f8681-196">Contiene inoltre il pacchetto che contiene una dipendenza da B A (> = 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="f8681-196">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="f8681-197">Si supponga che il progetto corrente dispone già di versione del pacchetto B 1.0.0 installato.</span><span class="sxs-lookup"><span data-stu-id="f8681-197">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="f8681-198">Ora si desidera installare a pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f8681-198">Now you want to install package A.</span></span>

<span data-ttu-id="f8681-199">**In NuGet 2.2 e versioni precedenti:**</span><span class="sxs-lookup"><span data-stu-id="f8681-199">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="f8681-200">Quando si installa un pacchetto, NuGet verrà aggiornata automaticamente B alla versione 1.0.2, anche se la versione 1.0.0 di esistente già soddisfa il vincolo di versione di dipendenza, è > = 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="f8681-200">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="f8681-201">**In NuGet 2.5 e versioni successive:**</span><span class="sxs-lookup"><span data-stu-id="f8681-201">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="f8681-202">NuGet non verrà più aggiornato B, perché viene rilevato che la versione esistente 1.0.0 soddisfa il vincolo di versione della dipendenza.</span><span class="sxs-lookup"><span data-stu-id="f8681-202">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="f8681-203">Per ulteriori informazioni su questa modifica, leggere la sezione dettagliata [elemento di lavoro](http://nuget.codeplex.com/workitem/1681) nonché correlata [thread di discussione](http://nuget.codeplex.com/discussions/436712).</span><span class="sxs-lookup"><span data-stu-id="f8681-203">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="f8681-204">NuGet.exe genera richieste http con livello di dettaglio massimo</span><span class="sxs-lookup"><span data-stu-id="f8681-204">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="f8681-205">Se si sta cercando di risolvere nuget.exe o semplicemente sapere quali richieste HTTP effettuate durante le operazioni di '-dettaglio dettagliata ' commutatore genera ora tutte le richieste HTTP effettuate.</span><span class="sxs-lookup"><span data-stu-id="f8681-205">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Output HTTP di nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="f8681-207">NuGet.exe push ora supporta origini UNC e cartella</span><span class="sxs-lookup"><span data-stu-id="f8681-207">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="f8681-208">Prima di NuGet 2.5, se si è tentato di eseguire 'nuget.exe push' a un'origine del pacchetto in base a un percorso UNC o una cartella locale, avrà esito negativo il push.</span><span class="sxs-lookup"><span data-stu-id="f8681-208">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="f8681-209">Con la funzionalità di configurazione gerarchici aggiunti di recente, diventa comune per nuget.exe devono necessariamente avere come destinazione un'origine o sulla cartella UNC o una raccolta di NuGet basato su HTTP.</span><span class="sxs-lookup"><span data-stu-id="f8681-209">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="f8681-210">A partire da NuGet 2.5, se nuget.exe identifica un'origine o sulla cartella UNC, viene eseguita la copia del file di origine.</span><span class="sxs-lookup"><span data-stu-id="f8681-210">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="f8681-211">Funzionamento dopo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f8681-211">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="f8681-212">NuGet.exe supporta i file di configurazione specificato in modo esplicito</span><span class="sxs-lookup"><span data-stu-id="f8681-212">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="f8681-213">i comandi di NuGet.exe che accedono a questo punto di configurazione (tutti ad eccezione di 'Mod' e 'pack') supportano un nuovo '-ConfigFile' opzione che impone un file di configurazione specifico da utilizzare al posto di file di configurazione predefinito % AppData%\nuget\Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="f8681-213">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="f8681-214">Esempio:</span><span class="sxs-lookup"><span data-stu-id="f8681-214">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="f8681-215">Supporto per i progetti nativi</span><span class="sxs-lookup"><span data-stu-id="f8681-215">Support for Native projects</span></span>

<span data-ttu-id="f8681-216">Con NuGet 2.5, gli strumenti di NuGet sono ora disponibili per i progetti nativi in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f8681-216">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="f8681-217">È probabile che più pacchetti nativi utilizzerà la funzionalità di importazioni di MSBuild, creato da uno strumento di [CoApp progetto](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="f8681-217">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="f8681-218">Per altre informazioni, vedere [informazioni sullo strumento](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) nel sito Web coapp.org.</span><span class="sxs-lookup"><span data-stu-id="f8681-218">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="f8681-219">Il nome del framework di destinazione di "nativa" è stato introdotto per i pacchetti includere file \build \content e \tools quando il pacchetto viene installato in un progetto nativo.</span><span class="sxs-lookup"><span data-stu-id="f8681-219">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="f8681-220">Il \`lib' cartella non viene utilizzata per i progetti nativi.</span><span class="sxs-lookup"><span data-stu-id="f8681-220">The \`lib` folder is not used for native projects.</span></span>
