---
title: Come creare un pacchetto per i controlli dell'interfaccia utente con NuGet
description: Come creare pacchetti NuGet contenenti controlli UWP o WPF, inclusi i metadati e i file di supporto necessari per le finestre di progettazione di Visual Studio e Blend.
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: 17062d83349fe1b8cd28e57dd888686a226ac9cb
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238023"
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="ba9cb-103">Creazione di controlli dell'interfaccia utente come pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="ba9cb-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="ba9cb-104">A partire da Visual Studio 2017, è possibile sfruttare le funzionalità aggiunte per i controlli UWP e WPF inseriti nei pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-104">Starting with Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="ba9cb-105">Questa guida illustra tali funzionalità nel contesto dei controlli UWP usando l'[esempio ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="ba9cb-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="ba9cb-106">Lo stesso vale per i controlli WPF, se non diversamente indicato.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba9cb-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ba9cb-107">Prerequisites</span></span>

1. <span data-ttu-id="ba9cb-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="ba9cb-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="ba9cb-109">Familiarità con la [creazione di pacchetti UWP](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="ba9cb-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="ba9cb-110">Generare il layout della libreria</span><span class="sxs-lookup"><span data-stu-id="ba9cb-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="ba9cb-111">Applicabile solo ai controlli UWP.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="ba9cb-112">L'impostazione della proprietà `GenerateLibraryLayout` garantisce che l'output di compilazione del progetto venga generato in un layout che è pronto per essere incluso nel pacchetto senza la necessità di voci per singoli file in nuspec.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="ba9cb-113">Dalle proprietà del progetto, passare alla scheda Build e selezionare la casella di controllo "Genera layout libreria".</span><span class="sxs-lookup"><span data-stu-id="ba9cb-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="ba9cb-114">Verrà modificato il file di progetto e il flag `GenerateLibraryLayout` verrà impostato su true per la configurazione e la piattaforma di compilazione attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="ba9cb-115">In alternativa, modificare il file di progetto per aggiungere `<GenerateLibraryLayout>true</GenerateLibraryLayout>` al primo gruppo di proprietà non condizionale.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="ba9cb-116">Questa modifica verrà applicata alla proprietà indipendentemente dalla configurazione o dalla piattaforma di compilazione.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="ba9cb-117">Aggiungere il supporto della casella degli strumenti e del riquadro Asset per i controlli XAML</span><span class="sxs-lookup"><span data-stu-id="ba9cb-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="ba9cb-118">Per visualizzare un controllo XAML nella casella degli strumenti della finestra di progettazione XAML in Visual Studio e nel riquadro Asset di Blend, creare un file `VisualStudioToolsManifest.xml` nella radice della cartella `tools` del progetto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="ba9cb-119">Questo file non è obbligatorio se non è necessario visualizzare il controllo nella casella degli strumenti o nel riquadro Asset.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="ba9cb-120">La struttura del file è la seguente:</span><span class="sxs-lookup"><span data-stu-id="ba9cb-120">The structure of the file is as follows:</span></span>

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems UIFramework="WPF" VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

<span data-ttu-id="ba9cb-121">dove:</span><span class="sxs-lookup"><span data-stu-id="ba9cb-121">where:</span></span>

- <span data-ttu-id="ba9cb-122">*your_package_file* : nome del file di controllo, ad esempio `ManagedPackage.winmd`. "ManagedPackage" è un nome arbitrario usato per questo esempio e non ha altri significati.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-122">*your_package_file* : the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="ba9cb-123">*vs_category* : etichetta del gruppo in cui il controllo deve essere visualizzato nella casella degli strumenti della finestra di progettazione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-123">*vs_category* : The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="ba9cb-124">`VSCategory` è necessario per visualizzare il controllo nella casella degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
<span data-ttu-id="ba9cb-125">*ui_framework* : il nome del Framework, ad esempio ' WPF ', si noti che `UIFramework` l'attributo è obbligatorio nei nodi ToolBoxItems in Visual Studio 16,7 Preview 3 o versione successiva affinché il controllo venga visualizzato nella casella degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-125">*ui_framework* : The name of the Framework, such as 'WPF', note that `UIFramework` attribute is required on ToolboxItems nodes on Visual Studio 16.7 Preview 3 or above for the control to appear in toolbox.</span></span>
- <span data-ttu-id="ba9cb-126">*blend_category* : etichetta del gruppo in cui il controllo deve essere visualizzato nel riquadro Asset della finestra di progettazione di Blend.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-126">*blend_category* : The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="ba9cb-127">`BlendCategory` è necessario per visualizzare il controllo in Asset.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-127">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="ba9cb-128">*type_full_name_n* : nome completo di ogni controllo, incluso lo spazio dei nomi, ad esempio `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-128">*type_full_name_n* : The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="ba9cb-129">Si noti che il formato punto viene usato sia per i tipi gestiti che per quelli nativi.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-129">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="ba9cb-130">Negli scenari più avanzati è anche possibile includere più elementi `<File>` in `<FileList>` quando un singolo pacchetto contiene più assembly del controllo.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-130">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="ba9cb-131">È anche possibile avere più nodi `<ToolboxItems>` in un singolo `<File>` se si vuole organizzare i controlli in categorie separate.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-131">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="ba9cb-132">Nell'esempio seguente il controllo implementato in `ManagedPackage.winmd` verrà visualizzato in Visual Studio e in Blend in un gruppo denominato "Managed Package" e "MyCustomControl" verrà visualizzato in tale gruppo.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-132">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="ba9cb-133">Tutti questi nomi sono arbitrari.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-133">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems UIFramework="WPF" VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Controllo di esempio visualizzato in Visual Studio](media/UWP-control-vs-toolbox.png)

![Controllo di esempio visualizzato in Blend](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="ba9cb-136">È necessario specificare in modo esplicito ogni controllo che si vuole visualizzare nella casella degli strumenti e nel riquadro Asset.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-136">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="ba9cb-137">Assicurarsi di specificarli nel formato `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-137">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="ba9cb-138">Aggiungere icone personalizzate ai controlli</span><span class="sxs-lookup"><span data-stu-id="ba9cb-138">Add custom icons to your controls</span></span>

<span data-ttu-id="ba9cb-139">Per visualizzare un'icona personalizzata nella casella degli strumenti e nel riquadro Asset, aggiungere un'immagine al proprio progetto o al corrispondente progetto `design.dll` con il nome "Namespace.ControlName.extension" e impostare l'azione di compilazione su "Risorsa incorporata".</span><span class="sxs-lookup"><span data-stu-id="ba9cb-139">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="ba9cb-140">È anche necessario assicurarsi che il file `AssemblyInfo.cs` associato specifichi l'attributo ProvideMetadata - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-140">You must also ensure that the associated `AssemblyInfo.cs` specifies the ProvideMetadata attribute - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span></span> <span data-ttu-id="ba9cb-141">Vedere questo [esempio](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span><span class="sxs-lookup"><span data-stu-id="ba9cb-141">See this [sample](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span></span>

<span data-ttu-id="ba9cb-142">I formati supportati sono `.png`, `.jpg`, `.jpeg`, `.gif` e `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-142">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="ba9cb-143">Il formato consigliato è BMP24 in 16 x 16 pixel.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-143">The recommended format is BMP24 in 16 pixels by 16 pixels.</span></span>

![Esempio di icona della casella degli strumenti](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

<span data-ttu-id="ba9cb-145">Lo sfondo di colore rosa viene sostituito in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-145">The pink background is replaced at runtime.</span></span> <span data-ttu-id="ba9cb-146">Le icone vengono ricolorate quando viene modificato il tema di Visual Studio e questo è il colore di sfondo previsto.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-146">The icons are recolored when the Visual Studio theme is changed and that background color is expected.</span></span> <span data-ttu-id="ba9cb-147">Per altre informazioni, vedere [Immagini e icone per Visual Studio](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="ba9cb-147">For more information, please reference [Images and Icons for Visual Studio](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span></span>

<span data-ttu-id="ba9cb-148">Nell'esempio seguente il progetto contiene un file di immagine denominato "ManagedPackage.MyCustomControl.png".</span><span class="sxs-lookup"><span data-stu-id="ba9cb-148">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Impostazione di un'icona personalizzata in un progetto](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="ba9cb-150">Per i controlli nativi, è necessario inserire l'icona come risorsa nel progetto `design.dll`.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-150">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="ba9cb-151">Supportare versioni specifiche della piattaforma Windows</span><span class="sxs-lookup"><span data-stu-id="ba9cb-151">Support specific Windows platform versions</span></span>

<span data-ttu-id="ba9cb-152">I pacchetti UWP hanno una proprietà TargetPlatformVersion (TPV) e una proprietà TargetPlatformMinVersion (TPMinV) che definiscono i limiti superiore e inferiore della versione del sistema operativo in cui l'app può essere installata.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-152">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="ba9cb-153">TPV specifica anche la versione dell'SDK in cui viene compilata l'app.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-153">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="ba9cb-154">Tenere sempre presente queste proprietà quando si crea un pacchetto UWP: usando API non comprese nei limiti delle versioni della piattaforma definite nell'app, non sarà possibile eseguire la compilazione o l'app avrà esito negativo in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-154">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="ba9cb-155">Si supponga, ad esempio, di avere impostato la proprietà TPMinV per il pacchetto dei controlli sull'edizione dell'anniversario di Windows 10 (10.0; build 14393) e di volersi quindi assicurare che il pacchetto venga utilizzato solo da progetti UWP che corrispondono a tale limite inferiore.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-155">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="ba9cb-156">Per consentire al pacchetto di essere utilizzato da progetti UWP, è necessario creare un pacchetto per i controlli con i nomi di cartella seguenti:</span><span class="sxs-lookup"><span data-stu-id="ba9cb-156">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="ba9cb-157">NuGet controllerà automaticamente la proprietà TPMinV del progetto che utilizza il pacchetto e l'installazione avrà esito negativo se il valore è inferiore a Windows 10 Anniversary Edition (10.0; build 14393)</span><span class="sxs-lookup"><span data-stu-id="ba9cb-157">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="ba9cb-158">Nel caso di WPF, si supponga di volere che il pacchetto dei controlli WPF venga utilizzato dai progetti destinati a .NET Framework v4.6.1 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-158">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="ba9cb-159">Per imporre questo requisito, è necessario creare un pacchetto dei controlli con i nomi di cartelle seguenti:</span><span class="sxs-lookup"><span data-stu-id="ba9cb-159">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="ba9cb-160">Aggiungere il supporto in fase di progettazione</span><span class="sxs-lookup"><span data-stu-id="ba9cb-160">Add design-time support</span></span>

<span data-ttu-id="ba9cb-161">Per configurare dove visualizzare le proprietà del controllo nel controllo proprietà, aggiungere gli strumenti decorativi personalizzati e così via e inserire il file `design.dll` nella cartella `lib\uap10.0.14393\Design` in modo appropriato alla piattaforma di destinazione.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-161">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="ba9cb-162">Per assicurarsi inoltre che la funzionalità **[Modifica modello > Modifica copia](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** operi correttamente, è necessario includere nella cartella `<your_assembly_name>\Themes``Generic.xaml` e tutti i dizionari risorse uniti, ancora una volta usando il nome di assembly effettivo.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-162">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="ba9cb-163">(Questo file non ha alcun effetto sul comportamento di runtime di un controllo). La struttura di cartelle viene quindi visualizzata come segue:</span><span class="sxs-lookup"><span data-stu-id="ba9cb-163">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="ba9cb-164">Nel caso di WPF, si supponga di continuare con l'esempio in cui si vuole che il pacchetto dei controlli WPF venga utilizzato dai progetti destinati a .NET Framework v4.6.1 o versione successiva:</span><span class="sxs-lookup"><span data-stu-id="ba9cb-164">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="ba9cb-165">Per impostazione predefinita, le proprietà del controllo verranno visualizzate sotto la categoria Varie nel controllo proprietà.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-165">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="ba9cb-166">Usare stringhe e risorse</span><span class="sxs-lookup"><span data-stu-id="ba9cb-166">Use strings and resources</span></span>

<span data-ttu-id="ba9cb-167">È possibile incorporare nel pacchetto le risorse stringa (`.resw`) che possono essere usate dal controllo o dal progetto UWP utilizzato e impostare la proprietà **Azione di compilazione** del file `.resw` su **PRIResource** .</span><span class="sxs-lookup"><span data-stu-id="ba9cb-167">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource** .</span></span>

<span data-ttu-id="ba9cb-168">Per un esempio, vedere [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) nell'esempio ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-168">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="ba9cb-169">Applicabile solo ai controlli UWP.</span><span class="sxs-lookup"><span data-stu-id="ba9cb-169">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="ba9cb-170">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ba9cb-170">See also</span></span>

- [<span data-ttu-id="ba9cb-171">Creare pacchetti UWP</span><span class="sxs-lookup"><span data-stu-id="ba9cb-171">Create UWP Packages</span></span>](create-uwp-packages.md)
- <span data-ttu-id="ba9cb-172">[ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage) (Esempio ExtensionSDKasNuGetPackage)</span><span class="sxs-lookup"><span data-stu-id="ba9cb-172">[ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)</span></span>