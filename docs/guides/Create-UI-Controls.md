---
title: Come creare un pacchetto per i controlli dell'interfaccia utente con NuGet
description: Come creare pacchetti NuGet contenenti controlli UWP o WPF, inclusi i metadati e i file di supporto necessari per le finestre di progettazione di Visual Studio e Blend.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: ab7499c415f63319fd314f33607f74d400b5f957
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818658"
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="2b640-103">Creazione di controlli dell'interfaccia utente come pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="2b640-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="2b640-104">Con Visual Studio 2017, è possibile sfruttare le funzionalità aggiunte per i controlli UWP e WPF inseriti nei pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="2b640-104">With Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="2b640-105">Questa guida illustra tali funzionalità nel contesto dei controlli UWP usando l'[esempio ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="2b640-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="2b640-106">Lo stesso vale per i controlli WPF, se non diversamente indicato.</span><span class="sxs-lookup"><span data-stu-id="2b640-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b640-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2b640-107">Prerequisites</span></span>

1. <span data-ttu-id="2b640-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="2b640-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="2b640-109">Familiarità con la [creazione di pacchetti UWP](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="2b640-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="2b640-110">Generare il layout della libreria</span><span class="sxs-lookup"><span data-stu-id="2b640-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="2b640-111">Applicabile solo ai controlli UWP.</span><span class="sxs-lookup"><span data-stu-id="2b640-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="2b640-112">L'impostazione della proprietà `GenerateLibraryLayout` garantisce che l'output di compilazione del progetto venga generato in un layout che è pronto per essere incluso nel pacchetto senza la necessità di voci per singoli file in nuspec.</span><span class="sxs-lookup"><span data-stu-id="2b640-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="2b640-113">Dalle proprietà del progetto, passare alla scheda Build e selezionare la casella di controllo "Genera layout libreria".</span><span class="sxs-lookup"><span data-stu-id="2b640-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="2b640-114">Verrà modificato il file di progetto e il flag `GenerateLibraryLayout` verrà impostato su true per la configurazione e la piattaforma di compilazione attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="2b640-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="2b640-115">In alternativa, modificare il file di progetto per aggiungere `<GenerateLibraryLayout>true</GenerateLibraryLayout>` al primo gruppo di proprietà non condizionale.</span><span class="sxs-lookup"><span data-stu-id="2b640-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="2b640-116">Questa modifica verrà applicata alla proprietà indipendentemente dalla configurazione o dalla piattaforma di compilazione.</span><span class="sxs-lookup"><span data-stu-id="2b640-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="2b640-117">Aggiungere il supporto della casella degli strumenti e del riquadro Asset per i controlli XAML</span><span class="sxs-lookup"><span data-stu-id="2b640-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="2b640-118">Per visualizzare un controllo XAML nella casella degli strumenti della finestra di progettazione XAML in Visual Studio e nel riquadro Asset di Blend, creare un file `VisualStudioToolsManifest.xml` nella radice della cartella `tools` del progetto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2b640-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="2b640-119">Questo file non è obbligatorio se non è necessario visualizzare il controllo nella casella degli strumenti o nel riquadro Asset.</span><span class="sxs-lookup"><span data-stu-id="2b640-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="2b640-120">La struttura del file è la seguente:</span><span class="sxs-lookup"><span data-stu-id="2b640-120">The structure of the file is as follows:</span></span>

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

<span data-ttu-id="2b640-121">dove:</span><span class="sxs-lookup"><span data-stu-id="2b640-121">where:</span></span>

- <span data-ttu-id="2b640-122">*your_package_file*: nome del file di controllo, ad esempio `ManagedPackage.winmd`. "ManagedPackage" è un nome arbitrario usato per questo esempio e non ha altri significati.</span><span class="sxs-lookup"><span data-stu-id="2b640-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="2b640-123">*vs_category*: etichetta del gruppo in cui il controllo deve essere visualizzato nella casella degli strumenti della finestra di progettazione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2b640-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="2b640-124">`VSCategory` è necessario per visualizzare il controllo nella casella degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="2b640-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="2b640-125">*blend_category*: etichetta del gruppo in cui il controllo deve essere visualizzato nel riquadro Asset della finestra di progettazione di Blend.</span><span class="sxs-lookup"><span data-stu-id="2b640-125">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="2b640-126">`BlendCategory` è necessario per visualizzare il controllo in Asset.</span><span class="sxs-lookup"><span data-stu-id="2b640-126">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="2b640-127">*type_full_name_n*: nome completo di ogni controllo, incluso lo spazio dei nomi, ad esempio `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="2b640-127">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="2b640-128">Si noti che il formato punto viene usato sia per i tipi gestiti che per quelli nativi.</span><span class="sxs-lookup"><span data-stu-id="2b640-128">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="2b640-129">Negli scenari più avanzati è anche possibile includere più elementi `<File>` in `<FileList>` quando un singolo pacchetto contiene più assembly del controllo.</span><span class="sxs-lookup"><span data-stu-id="2b640-129">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="2b640-130">È anche possibile avere più nodi `<ToolboxItems>` in un singolo `<File>` se si vuole organizzare i controlli in categorie separate.</span><span class="sxs-lookup"><span data-stu-id="2b640-130">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="2b640-131">Nell'esempio seguente il controllo implementato in `ManagedPackage.winmd` verrà visualizzato in Visual Studio e in Blend in un gruppo denominato "Managed Package" e "MyCustomControl" verrà visualizzato in tale gruppo.</span><span class="sxs-lookup"><span data-stu-id="2b640-131">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="2b640-132">Tutti questi nomi sono arbitrari.</span><span class="sxs-lookup"><span data-stu-id="2b640-132">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Controllo di esempio visualizzato in Visual Studio](media/UWP-control-vs-toolbox.png)

![Controllo di esempio visualizzato in Blend](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="2b640-135">È necessario specificare in modo esplicito ogni controllo che si vuole visualizzare nella casella degli strumenti e nel riquadro Asset.</span><span class="sxs-lookup"><span data-stu-id="2b640-135">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="2b640-136">Assicurarsi di specificarli nel formato `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="2b640-136">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="2b640-137">Aggiungere icone personalizzate ai controlli</span><span class="sxs-lookup"><span data-stu-id="2b640-137">Add custom icons to your controls</span></span>

<span data-ttu-id="2b640-138">Per visualizzare un'icona personalizzata nella casella degli strumenti e nel riquadro Asset, aggiungere un'immagine al proprio progetto o al corrispondente progetto `design.dll` con il nome "Namespace.ControlName.extension" e impostare l'azione di compilazione su "Risorsa incorporata".</span><span class="sxs-lookup"><span data-stu-id="2b640-138">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="2b640-139">I formati supportati sono `.png`, `.jpg`, `.jpeg`, `.gif` e `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="2b640-139">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="2b640-140">Le dimensioni dell'immagine consigliate sono pari a 64 x 64 pixel.</span><span class="sxs-lookup"><span data-stu-id="2b640-140">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="2b640-141">Nell'esempio seguente il progetto contiene un file di immagine denominato "ManagedPackage.MyCustomControl.png".</span><span class="sxs-lookup"><span data-stu-id="2b640-141">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Impostazione di un'icona personalizzata in un progetto](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="2b640-143">Per i controlli nativi, è necessario inserire l'icona come risorsa nel progetto `design.dll`.</span><span class="sxs-lookup"><span data-stu-id="2b640-143">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="2b640-144">Supportare versioni specifiche della piattaforma Windows</span><span class="sxs-lookup"><span data-stu-id="2b640-144">Support specific Windows platform versions</span></span>

<span data-ttu-id="2b640-145">I pacchetti UWP hanno una proprietà TargetPlatformVersion (TPV) e una proprietà TargetPlatformMinVersion (TPMinV) che definiscono i limiti superiore e inferiore della versione del sistema operativo in cui l'app può essere installata.</span><span class="sxs-lookup"><span data-stu-id="2b640-145">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="2b640-146">TPV specifica anche la versione dell'SDK in cui viene compilata l'app.</span><span class="sxs-lookup"><span data-stu-id="2b640-146">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="2b640-147">Tenere sempre presente queste proprietà quando si crea un pacchetto UWP: usando API non comprese nei limiti delle versioni della piattaforma definite nell'app, non sarà possibile eseguire la compilazione o l'app avrà esito negativo in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2b640-147">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="2b640-148">Si supponga, ad esempio, di avere impostato la proprietà TPMinV per il pacchetto dei controlli sull'edizione dell'anniversario di Windows 10 (10.0; build 14393) e di volersi quindi assicurare che il pacchetto venga utilizzato solo da progetti UWP che corrispondono a tale limite inferiore.</span><span class="sxs-lookup"><span data-stu-id="2b640-148">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="2b640-149">Per consentire al pacchetto di essere utilizzato da progetti UWP, è necessario creare un pacchetto per i controlli con i nomi di cartella seguenti:</span><span class="sxs-lookup"><span data-stu-id="2b640-149">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="2b640-150">NuGet controllerà automaticamente la proprietà TPMinV del progetto che utilizza il pacchetto e l'installazione avrà esito negativo se il valore è inferiore a Windows 10 Anniversary Edition (10.0; build 14393)</span><span class="sxs-lookup"><span data-stu-id="2b640-150">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="2b640-151">Nel caso di WPF, si supponga di volere che il pacchetto dei controlli WPF venga utilizzato dai progetti destinati a .NET Framework v4.6.1 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="2b640-151">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="2b640-152">Per imporre questo requisito, è necessario creare un pacchetto dei controlli con i nomi di cartelle seguenti:</span><span class="sxs-lookup"><span data-stu-id="2b640-152">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="2b640-153">Aggiungere il supporto in fase di progettazione</span><span class="sxs-lookup"><span data-stu-id="2b640-153">Add design-time support</span></span>

<span data-ttu-id="2b640-154">Per configurare dove visualizzare le proprietà del controllo nel controllo proprietà, aggiungere gli strumenti decorativi personalizzati e così via e inserire il file `design.dll` nella cartella `lib\uap10.0.14393\Design` in modo appropriato alla piattaforma di destinazione.</span><span class="sxs-lookup"><span data-stu-id="2b640-154">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="2b640-155">Per assicurarsi inoltre che la funzionalità **[Modifica modello > Modifica copia](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** operi correttamente, è necessario includere nella cartella `<your_assembly_name>\Themes` `Generic.xaml` e tutti i dizionari risorse uniti, ancora una volta usando il nome di assembly effettivo.</span><span class="sxs-lookup"><span data-stu-id="2b640-155">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="2b640-156">Questo file non influisce sul comportamento di runtime di un controllo. La struttura di cartelle avrà quindi l'aspetto seguente:</span><span class="sxs-lookup"><span data-stu-id="2b640-156">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="2b640-157">Nel caso di WPF, si supponga di continuare con l'esempio in cui si vuole che il pacchetto dei controlli WPF venga utilizzato dai progetti destinati a .NET Framework v4.6.1 o versione successiva:</span><span class="sxs-lookup"><span data-stu-id="2b640-157">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="2b640-158">Per impostazione predefinita, le proprietà del controllo verranno visualizzate sotto la categoria Varie nel controllo proprietà.</span><span class="sxs-lookup"><span data-stu-id="2b640-158">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="2b640-159">Usare stringhe e risorse</span><span class="sxs-lookup"><span data-stu-id="2b640-159">Use strings and resources</span></span>

<span data-ttu-id="2b640-160">È possibile incorporare nel pacchetto le risorse stringa (`.resw`) che possono essere usate dal controllo o dal progetto UWP utilizzato e impostare la proprietà **Azione di compilazione** del file `.resw` su **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="2b640-160">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="2b640-161">Per un esempio, vedere [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) nell'esempio ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="2b640-161">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="2b640-162">Applicabile solo ai controlli UWP.</span><span class="sxs-lookup"><span data-stu-id="2b640-162">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="2b640-163">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2b640-163">See also</span></span>

- [<span data-ttu-id="2b640-164">Creare pacchetti UWP</span><span class="sxs-lookup"><span data-stu-id="2b640-164">Create UWP Packages</span></span>](create-uwp-packages.md)
- <span data-ttu-id="2b640-165">[ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage) (Esempio ExtensionSDKasNuGetPackage)</span><span class="sxs-lookup"><span data-stu-id="2b640-165">[ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)</span></span>
