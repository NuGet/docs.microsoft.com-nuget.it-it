---
title: Note sulla versione di NuGet 2,5
description: Note sulla versione per NuGet 2,5, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940582d5173f5a53dcd04cf1258fc02a2439af4e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237083"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="a455e-103">Note sulla versione di NuGet 2,5</span><span class="sxs-lookup"><span data-stu-id="a455e-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="a455e-104">Note sulla versione di [NuGet 2.2.1](../release-notes/nuget-2.2.1.md)  |  [Note sulla versione di NuGet 2,6](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="a455e-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="a455e-105">NuGet 2,5 è stato rilasciato il 25 aprile 2013.</span><span class="sxs-lookup"><span data-stu-id="a455e-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="a455e-106">Questa versione era così grande. ci si era costretti a ignorare le versioni 2,3 e 2,4.</span><span class="sxs-lookup"><span data-stu-id="a455e-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="a455e-107">Fino a oggi, questa è la versione più grande disponibile per NuGet, con oltre [160 elementi di lavoro](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) nella versione.</span><span class="sxs-lookup"><span data-stu-id="a455e-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="a455e-108">Riconoscimenti</span><span class="sxs-lookup"><span data-stu-id="a455e-108">Acknowledgements</span></span>

<span data-ttu-id="a455e-109">Vorremmo ringraziare i collaboratori esterni seguenti per i contributi significativi a NuGet 2,5:</span><span class="sxs-lookup"><span data-stu-id="a455e-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="a455e-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ( [@dsplaisted](https://twitter.com/dsplaisted) )</span><span class="sxs-lookup"><span data-stu-id="a455e-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="a455e-111">[#2847](https://nuget.codeplex.com/workitem/2847) : aggiungere monoandroid, MonoTouch e MonoMac all'elenco di identificatori di Framework di destinazione noti.</span><span class="sxs-lookup"><span data-stu-id="a455e-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="a455e-112">[Andres G. Aragonesi](https://www.codeplex.com/site/users/view/knocte) ( [@knocte](https://twitter.com/knocte) )</span><span class="sxs-lookup"><span data-stu-id="a455e-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="a455e-113">[#2865](https://nuget.codeplex.com/workitem/2865) correggere l'ortografia di `NuGet.targets` per un sistema operativo con distinzione tra maiuscole e minuscole</span><span class="sxs-lookup"><span data-stu-id="a455e-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="a455e-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ( [@davidfowl](https://twitter.com/davidfowl) )</span><span class="sxs-lookup"><span data-stu-id="a455e-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="a455e-115">Creare la soluzione in mono.</span><span class="sxs-lookup"><span data-stu-id="a455e-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="a455e-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ( [@atheken](https://twitter.com/atheken) )</span><span class="sxs-lookup"><span data-stu-id="a455e-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="a455e-117">Correzione degli unit test con errore in mono.</span><span class="sxs-lookup"><span data-stu-id="a455e-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="a455e-118">[Olivier Bellis](https://www.codeplex.com/site/users/view/OliIsCool) ( [@OliIsCool](https://twitter.com/oliiscool) )</span><span class="sxs-lookup"><span data-stu-id="a455e-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="a455e-119">il comando [#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe Pack non propaga le proprietà a MSBuild</span><span class="sxs-lookup"><span data-stu-id="a455e-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="a455e-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ( [@bajtos](https://twitter.com/bajtos) )</span><span class="sxs-lookup"><span data-stu-id="a455e-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="a455e-121">[#1511](https://nuget.codeplex.com/workitem/1511) modificare il codice di gestione XML per mantenere la formattazione.</span><span class="sxs-lookup"><span data-stu-id="a455e-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="a455e-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )</span><span class="sxs-lookup"><span data-stu-id="a455e-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="a455e-123">Sono state aggiunte parole riconosciute al dizionario personalizzato per consentire a Build. cmd di avere esito positivo.</span><span class="sxs-lookup"><span data-stu-id="a455e-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="a455e-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="a455e-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="a455e-125">Correzione degli unit test durante l'esecuzione in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a455e-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="a455e-126">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="a455e-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="a455e-127">Interfaccia estratta da PackageService</span><span class="sxs-lookup"><span data-stu-id="a455e-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="a455e-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ( [@brugidou](https://twitter.com/brugidou) )</span><span class="sxs-lookup"><span data-stu-id="a455e-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="a455e-129">[#936](https://nuget.codeplex.com/workitem/936) gestire le dipendenze di progetto durante la compressione</span><span class="sxs-lookup"><span data-stu-id="a455e-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="a455e-130">[Decostore Xavier](https://www.codeplex.com/site/users/view/XavierDecoster) ( [@XavierDecoster](https://twitter.com/xavierdecoster) )</span><span class="sxs-lookup"><span data-stu-id="a455e-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="a455e-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) supporta la password non crittografata durante l'archiviazione delle credenziali di origine del pacchetto nei file NuGet. cofig</span><span class="sxs-lookup"><span data-stu-id="a455e-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="a455e-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ( [@manningj](https://twitter.com/manningj) )</span><span class="sxs-lookup"><span data-stu-id="a455e-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="a455e-133">[#3190](http://nuget.codeplex.com/workitem/3190), correzione [#3191](http://nuget.codeplex.com/workitem/3191) Get-Package Descrizione della Guida</span><span class="sxs-lookup"><span data-stu-id="a455e-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="a455e-134">Sono inoltre apprezzate le persone seguenti per individuare i bug con NuGet 2,5 beta/RC che sono stati approvati e corretti prima della versione finale:</span><span class="sxs-lookup"><span data-stu-id="a455e-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="a455e-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ( [@CodeChief](https://twitter.com/codechief) )</span><span class="sxs-lookup"><span data-stu-id="a455e-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="a455e-136">[#3200](https://nuget.codeplex.com/workitem/3200) -MSTest interruppe con le compilazioni NuGet 2,4 e 2,5 più recenti</span><span class="sxs-lookup"><span data-stu-id="a455e-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="a455e-137">Funzionalità rilevanti della versione</span><span class="sxs-lookup"><span data-stu-id="a455e-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="a455e-138">Consenti agli utenti di sovrascrivere i file di contenuto già esistenti</span><span class="sxs-lookup"><span data-stu-id="a455e-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="a455e-139">Una delle funzionalità più richieste di tutti i tempi è la possibilità di sovrascrivere i file di contenuto già presenti sul disco quando sono inclusi in un pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="a455e-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="a455e-140">A partire da NuGet 2,5, questi conflitti vengono identificati e viene richiesto di sovrascrivere i file, mentre in precedenza questi file venivano sempre ignorati.</span><span class="sxs-lookup"><span data-stu-id="a455e-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Sovrascrivi file di contenuto](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="a455e-142">' nuget.exe Update ' è Install-Package ' dispongono ora di una nuova opzione '-FileConflictAction ' per impostare alcune impostazioni predefinite per gli scenari da riga di comando.</span><span class="sxs-lookup"><span data-stu-id="a455e-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="a455e-143">Impostare un'azione predefinita quando un file di un pacchetto esiste già nel progetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="a455e-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="a455e-144">Impostare su' Sovrascrivi ' per sovrascrivere sempre i file.</span><span class="sxs-lookup"><span data-stu-id="a455e-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="a455e-145">Impostare su' ignore ' per ignorare i file.</span><span class="sxs-lookup"><span data-stu-id="a455e-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="a455e-146">Se non è specificato, verrà richiesto di specificare ogni file in conflitto.</span><span class="sxs-lookup"><span data-stu-id="a455e-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="a455e-147">Importazione automatica di file di destinazione e Props di MSBuild</span><span class="sxs-lookup"><span data-stu-id="a455e-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="a455e-148">È stata creata una nuova cartella convenzionale al livello principale del pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="a455e-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="a455e-149">Come peer per `\lib` , `\content` e `\tools` , è ora possibile includere una `\build` cartella nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a455e-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="a455e-150">In questa cartella è possibile inserire due file con nomi fissi `{packageid}.targets` o `{packageid}.props` .</span><span class="sxs-lookup"><span data-stu-id="a455e-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="a455e-151">Questi due file possono essere direttamente in `build` o in cartelle specifiche del Framework come le altre cartelle.</span><span class="sxs-lookup"><span data-stu-id="a455e-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="a455e-152">La regola per la selezione della cartella del Framework con la corrispondenza più appropriata è esattamente identica a quella di.</span><span class="sxs-lookup"><span data-stu-id="a455e-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="a455e-153">Quando NuGet installa un pacchetto con i file \Build, viene aggiunto un `<Import>` elemento MSBuild nel file di progetto che punta ai `.targets` `.props` file e.</span><span class="sxs-lookup"><span data-stu-id="a455e-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="a455e-154">Il `.props` file viene aggiunto nella parte superiore, mentre il `.targets` file viene aggiunto alla fine.</span><span class="sxs-lookup"><span data-stu-id="a455e-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="a455e-155">Specificare diversi riferimenti per piattaforma usando l' `<References/>` elemento</span><span class="sxs-lookup"><span data-stu-id="a455e-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="a455e-156">Prima del 2,5, in `.nuspec` file, l'utente può specificare solo i file di riferimento da aggiungere per tutti i Framework.</span><span class="sxs-lookup"><span data-stu-id="a455e-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="a455e-157">Ora, con questa nuova funzionalità di 2,5, l'utente può creare l' `<reference/>` elemento per ogni piattaforma supportata, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a455e-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

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

<span data-ttu-id="a455e-158">Ecco il flusso per il modo in cui NuGet aggiunge i riferimenti ai progetti in base al `.nuspec` file:</span><span class="sxs-lookup"><span data-stu-id="a455e-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="a455e-159">Individuare la `lib` cartella appropriata per il Framework di destinazione e ottenere l'elenco degli assembly da tale cartella</span><span class="sxs-lookup"><span data-stu-id="a455e-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="a455e-160">Trovare separatamente il gruppo References appropriato per il Framework di destinazione e ottenere l'elenco degli assembly dal gruppo.</span><span class="sxs-lookup"><span data-stu-id="a455e-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="a455e-161">Gruppo di riferimento senza Framework di destinazione specificato è il gruppo di fallback.</span><span class="sxs-lookup"><span data-stu-id="a455e-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="a455e-162">Trovare l'intersezione dei due elenchi e usarla come riferimento da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="a455e-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="a455e-163">Questa nuova funzionalità consentirà agli autori di pacchetti di utilizzare la funzionalità riferimenti per applicare subset di assembly a Framework diversi quando sarebbe altrimenti necessario eseguire assembly duplicati in più `lib` cartelle.</span><span class="sxs-lookup"><span data-stu-id="a455e-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="a455e-164">Nota: per usare questa funzionalità, è necessario usare attualmente nuget.exe Pack. Gestione pacchetti NuGet non supporta ancora questa operazione.</span><span class="sxs-lookup"><span data-stu-id="a455e-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="a455e-165">Pulsante Aggiorna tutto per consentire l'aggiornamento di tutti i pacchetti contemporaneamente</span><span class="sxs-lookup"><span data-stu-id="a455e-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="a455e-166">Molti di voi conoscono il cmdlet di PowerShell "Update-Package" per aggiornare tutti i pacchetti; ora esiste un modo semplice per eseguire questa operazione anche tramite l'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="a455e-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="a455e-167">Per provare questa funzionalità:</span><span class="sxs-lookup"><span data-stu-id="a455e-167">To try this feature out:</span></span>

1. <span data-ttu-id="a455e-168">Creare una nuova applicazione MVC ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a455e-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="a455e-169">Avvia la finestra di dialogo ' Gestisci pacchetti NuGet '</span><span class="sxs-lookup"><span data-stu-id="a455e-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="a455e-170">Selezionare ' aggiornamenti '</span><span class="sxs-lookup"><span data-stu-id="a455e-170">Select 'Updates'</span></span>
1. <span data-ttu-id="a455e-171">Fai clic sul pulsante ' Aggiorna tutto '</span><span class="sxs-lookup"><span data-stu-id="a455e-171">Click the 'Update All' button</span></span>

![Pulsante Aggiorna tutto nella finestra di dialogo](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="a455e-173">Supporto migliorato per il riferimento al progetto per nuget.exe Pack</span><span class="sxs-lookup"><span data-stu-id="a455e-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="a455e-174">A questo punto, nuget.exe comando Pack elabora i progetti a cui si fa riferimento con le regole seguenti:</span><span class="sxs-lookup"><span data-stu-id="a455e-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="a455e-175">Se nel progetto a cui si fa riferimento è `.nuspec` presente un file corrispondente, ad esempio è presente un file denominato `proj1.nuspec` nella stessa cartella di `proj1.csproj` , questo progetto viene aggiunto come dipendenza al pacchetto, usando l'ID e la versione letti dal `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="a455e-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="a455e-176">In caso contrario, i file del progetto a cui si fa riferimento vengono aggregati nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a455e-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="a455e-177">I progetti a cui fa riferimento questo progetto verranno elaborati con le stesse regole in modo ricorsivo.</span><span class="sxs-lookup"><span data-stu-id="a455e-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="a455e-178">`.pdb` `.exe` Vengono aggiunti tutti i file dll, e.</span><span class="sxs-lookup"><span data-stu-id="a455e-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="a455e-179">Tutti gli altri file di contenuto vengono aggiunti.</span><span class="sxs-lookup"><span data-stu-id="a455e-179">All other content files are added.</span></span>
1. <span data-ttu-id="a455e-180">Tutte le dipendenze sono unite.</span><span class="sxs-lookup"><span data-stu-id="a455e-180">All dependencies are merged.</span></span>

<span data-ttu-id="a455e-181">Ciò consente a un progetto a cui si fa riferimento di essere considerato come una dipendenza se è presente un `.nuspec` file, in caso contrario, diventa parte del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a455e-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="a455e-182">Altre informazioni sono disponibili qui: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="a455e-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="a455e-183">Aggiungere una proprietà' versione minima di NuGet ' ai pacchetti</span><span class="sxs-lookup"><span data-stu-id="a455e-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="a455e-184">Un nuovo attributo di metadati denominato ' minClientVersion ' può ora indicare la versione minima del client NuGet necessaria per l'utilizzo di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a455e-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="a455e-185">Questa funzionalità consente all'autore del pacchetto di specificare che un pacchetto funzionerà solo dopo una particolare versione di NuGet.</span><span class="sxs-lookup"><span data-stu-id="a455e-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="a455e-186">Quando `.nuspec` si aggiungono nuove funzionalità dopo NuGet 2,5, i pacchetti saranno in grado di richiedere una versione minima di NuGet.</span><span class="sxs-lookup"><span data-stu-id="a455e-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="a455e-187">Se l'utente ha installato NuGet 2,5 e un pacchetto viene identificato con la richiesta 2,6, i segnali visivi verranno assegnati all'utente che indica che il pacchetto non sarà installabile.</span><span class="sxs-lookup"><span data-stu-id="a455e-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="a455e-188">L'utente verrà quindi guidato per aggiornare la versione di NuGet.</span><span class="sxs-lookup"><span data-stu-id="a455e-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="a455e-189">Ciò consente di migliorare l'esperienza esistente in cui i pacchetti iniziano l'installazione, ma non indica che è stata identificata una versione dello schema non riconosciuta.</span><span class="sxs-lookup"><span data-stu-id="a455e-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="a455e-190">Non è più necessario aggiornare le dipendenze durante l'installazione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="a455e-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="a455e-191">Prima di NuGet 2,5, quando è stato installato un pacchetto che dipende da un pacchetto già installato nel progetto, la dipendenza verrebbe aggiornata come parte della nuova installazione, anche se la versione esistente soddisfa la dipendenza.</span><span class="sxs-lookup"><span data-stu-id="a455e-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="a455e-192">A partire da NuGet 2,5, se è già stata soddisfatta una versione di dipendenza, la dipendenza non verrà aggiornata durante le altre installazioni del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a455e-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="a455e-193">**Scenario:**</span><span class="sxs-lookup"><span data-stu-id="a455e-193">**The scenario:**</span></span>

1. <span data-ttu-id="a455e-194">Il repository di origine contiene il pacchetto B con versione 1.0.0 e 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="a455e-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="a455e-195">Contiene anche il pacchetto A che ha una dipendenza da B (>= 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="a455e-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="a455e-196">Si supponga che nel progetto corrente sia già installato il pacchetto B versione 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="a455e-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="a455e-197">A questo punto si vuole installare il pacchetto A.</span><span class="sxs-lookup"><span data-stu-id="a455e-197">Now you want to install package A.</span></span>

<span data-ttu-id="a455e-198">**In NuGet 2,2 e versioni precedenti:**</span><span class="sxs-lookup"><span data-stu-id="a455e-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="a455e-199">Quando si installa il pacchetto A, NuGet aggiorna automaticamente B a 1.0.2, anche se la versione esistente 1.0.0 soddisfa già il vincolo della versione di dipendenza, che è >= 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="a455e-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="a455e-200">**In NuGet 2,5 e versioni successive:**</span><span class="sxs-lookup"><span data-stu-id="a455e-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="a455e-201">NuGet non aggiornerà più B, perché rileva che la versione esistente 1.0.0 soddisfa il vincolo della versione di dipendenza.</span><span class="sxs-lookup"><span data-stu-id="a455e-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="a455e-202">Per ulteriori informazioni su questa modifica, leggere l' [elemento di lavoro](http://nuget.codeplex.com/workitem/1681) dettagliato e il thread di [discussione](http://nuget.codeplex.com/discussions/436712)correlato.</span><span class="sxs-lookup"><span data-stu-id="a455e-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="a455e-203">nuget.exe restituisce richieste HTTP con dettaglio dettagliato</span><span class="sxs-lookup"><span data-stu-id="a455e-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="a455e-204">Per la risoluzione dei problemi nuget.exe o solo per le richieste HTTP eseguite durante le operazioni, l'opzione '-verbose detailed ' ora restituirà tutte le richieste HTTP effettuate.</span><span class="sxs-lookup"><span data-stu-id="a455e-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Output HTTP da nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="a455e-206">nuget.exe push supporta ora le origini UNC e delle cartelle</span><span class="sxs-lookup"><span data-stu-id="a455e-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="a455e-207">Prima di NuGet 2,5, se si tentasse di eseguire ' nuget.exe push ' in un'origine del pacchetto basata su un percorso UNC o una cartella locale, il push avrebbe esito negativo.</span><span class="sxs-lookup"><span data-stu-id="a455e-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="a455e-208">Con la funzionalità di configurazione gerarchica aggiunta di recente, era diventata comune per nuget.exe la necessità di specificare come destinazione un'origine UNC/cartella o una raccolta NuGet basata su HTTP.</span><span class="sxs-lookup"><span data-stu-id="a455e-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="a455e-209">A partire da NuGet 2,5, se nuget.exe identifica un'origine UNC/cartella, eseguirà la copia del file nell'origine.</span><span class="sxs-lookup"><span data-stu-id="a455e-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="a455e-210">Il comando seguente funzionerà ora:</span><span class="sxs-lookup"><span data-stu-id="a455e-210">The following command will now work:</span></span>

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="a455e-211">nuget.exe supporta i file di configurazione specificati in modo esplicito</span><span class="sxs-lookup"><span data-stu-id="a455e-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="a455e-212">nuget.exe comandi che accedono alla configurazione (tutti tranne ' spec ' è Pack ') supportano ora una nuova opzione '-ConfigFile ', che impone l'uso di un file di configurazione specifico al posto del file di configurazione predefinito in% AppData% \nuget\Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="a455e-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="a455e-213">Esempio:</span><span class="sxs-lookup"><span data-stu-id="a455e-213">Example:</span></span>

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="a455e-214">Supporto per progetti nativi</span><span class="sxs-lookup"><span data-stu-id="a455e-214">Support for Native projects</span></span>

<span data-ttu-id="a455e-215">Con NuGet 2,5, gli strumenti NuGet sono ora disponibili per i progetti nativi in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a455e-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="a455e-216">Si prevede che la maggior parte dei pacchetti nativi utilizzerà la funzionalità di importazione di MSBuild precedente, usando uno strumento creato dal [progetto CoApp](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="a455e-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="a455e-217">Per ulteriori informazioni, leggere [i dettagli sullo strumento](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) nel sito Web coapp.org.</span><span class="sxs-lookup"><span data-stu-id="a455e-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="a455e-218">Il nome del Framework di destinazione "native" è stato introdotto per i pacchetti in modo da includere i file in \Build, \Content e \Tools quando il pacchetto viene installato in un progetto nativo.</span><span class="sxs-lookup"><span data-stu-id="a455e-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="a455e-219">La \` cartella lib ' non viene utilizzata per i progetti nativi.</span><span class="sxs-lookup"><span data-stu-id="a455e-219">The \`lib\` folder is not used for native projects.</span></span>
