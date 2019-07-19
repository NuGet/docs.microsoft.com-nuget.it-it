---
title: Identificare il formato del progetto
description: Viene descritto come identificare il formato del progetto
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 3d8745ea30115a2d7f3954d171d92b75a434a55b
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843443"
---
# <a name="identify-the-project-format"></a><span data-ttu-id="08767-103">Identificare il formato del progetto</span><span class="sxs-lookup"><span data-stu-id="08767-103">Identify the project format</span></span>

<span data-ttu-id="08767-104">NuGet supporta tutti i progetti .NET.</span><span class="sxs-lookup"><span data-stu-id="08767-104">NuGet works with all .NET projects.</span></span> <span data-ttu-id="08767-105">Tuttavia, il formato del progetto (di tipo SDK o non in SDK) determina alcuni degli strumenti e dei metodi che è necessario usare per utilizzare e creare pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="08767-105">However, the project format (SDK-style or non-SDK-style) determines some of the tools and methods that you need to use to consume and create NuGet packages.</span></span> <span data-ttu-id="08767-106">I progetti di tipo SDK usano l'[attributo SDK](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="08767-106">SDK-style projects use the [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span> <span data-ttu-id="08767-107">È importante identificare il tipo di progetto perché i metodi e gli strumenti usati per utilizzare e creare pacchetti NuGet dipendono dal formato del progetto.</span><span class="sxs-lookup"><span data-stu-id="08767-107">It is important to identify your project type because the methods and tools you use to consume and create NuGet packages are dependent on the project format.</span></span> <span data-ttu-id="08767-108">Per i progetti non di tipo SDK, i metodi e gli strumenti dipendono anche dal fatto che sia stata eseguita la migrazione del progetto al formato `PackageReference`.</span><span class="sxs-lookup"><span data-stu-id="08767-108">For non-SDK-style projects, the methods and tools are also dependent on whether or not the project has been migrated to `PackageReference` format.</span></span>

<span data-ttu-id="08767-109">Il fatto che il progetto sia o meno di tipo SDK dipende dal metodo usato per creare il progetto.</span><span class="sxs-lookup"><span data-stu-id="08767-109">Whether your project is SDK-style or not depends on the method used to create the project.</span></span> <span data-ttu-id="08767-110">La tabella seguente mostra il formato di progetto predefinito e lo strumento dell'interfaccia della riga di comando associato per il progetto quando lo si crea con Visual Studio 2017 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="08767-110">The following table shows the default project format and the associated CLI tool for your project when you create it using Visual Studio 2017 and later versions.</span></span>

| <span data-ttu-id="08767-111">Progetto&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="08767-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="08767-112">Formato progetto predefinito</span><span class="sxs-lookup"><span data-stu-id="08767-112">Default project format</span></span> | <span data-ttu-id="08767-113">Strumento dell'interfaccia della riga di comando&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="08767-113">CLI tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="08767-114">Note</span><span class="sxs-lookup"><span data-stu-id="08767-114">Notes</span></span> |
|:------------- |:-------------|:-----|:-----|
| <span data-ttu-id="08767-115">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="08767-115">.NET Standard</span></span> | <span data-ttu-id="08767-116">Stile SDK</span><span class="sxs-lookup"><span data-stu-id="08767-116">SDK-style</span></span> | [<span data-ttu-id="08767-117">Interfaccia della riga di comando di dotnet</span><span class="sxs-lookup"><span data-stu-id="08767-117">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="08767-118">I progetti creati prima di Visual Studio 2017 non sono di tipo SDK.</span><span class="sxs-lookup"><span data-stu-id="08767-118">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="08767-119">Usare l'interfaccia della riga di comando `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="08767-119">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="08767-120">.NET Core</span><span class="sxs-lookup"><span data-stu-id="08767-120">.NET Core</span></span> | <span data-ttu-id="08767-121">Stile SDK</span><span class="sxs-lookup"><span data-stu-id="08767-121">SDK-style</span></span> | [<span data-ttu-id="08767-122">Interfaccia della riga di comando di dotnet</span><span class="sxs-lookup"><span data-stu-id="08767-122">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="08767-123">I progetti creati prima di Visual Studio 2017 non sono di tipo SDK.</span><span class="sxs-lookup"><span data-stu-id="08767-123">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="08767-124">Usare l'interfaccia della riga di comando `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="08767-124">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="08767-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="08767-125">.NET Framework</span></span> | <span data-ttu-id="08767-126">Non di tipo SDK</span><span class="sxs-lookup"><span data-stu-id="08767-126">Non-SDK-style</span></span> | [<span data-ttu-id="08767-127">Interfaccia della riga di comando di nuget.exe</span><span class="sxs-lookup"><span data-stu-id="08767-127">nuget.exe CLI</span></span>](../install-nuget-client-tools.md#nugetexe-cli) | <span data-ttu-id="08767-128">I progetti .NET Framework creati con altri metodi possono essere progetti di tipo SDK.</span><span class="sxs-lookup"><span data-stu-id="08767-128">.NET Framework projects created using other methods may be SDK-style projects.</span></span> <span data-ttu-id="08767-129">Per questi progetti, usare invece l'[interfaccia della riga di comando dotnet](../install-nuget-client-tools.md#dotnetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="08767-129">For these, use [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) instead.</span></span> |
| <span data-ttu-id="08767-130">Progetto .NET [migrato](../reference/migrate-packages-config-to-package-reference.md)</span><span class="sxs-lookup"><span data-stu-id="08767-130">[Migrated](../reference/migrate-packages-config-to-package-reference.md) .NET project</span></span> | <span data-ttu-id="08767-131">Non di tipo SDK</span><span class="sxs-lookup"><span data-stu-id="08767-131">Non-SDK-style</span></span>| <span data-ttu-id="08767-132">Per creare pacchetti, usare [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="08767-132">To create packages, use [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) to create packages.</span></span> | <span data-ttu-id="08767-133">Per creare pacchetti, è consigliabile usare `msbuild -t:pack`.</span><span class="sxs-lookup"><span data-stu-id="08767-133">To create packages, `msbuild -t:pack` is recommended.</span></span> <span data-ttu-id="08767-134">Altrimenti, usare l'[interfaccia della riga di comando dotnet](../install-nuget-client-tools.md#dotnetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="08767-134">Otherwise, use the [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span></span> <span data-ttu-id="08767-135">I progetti migrati sono progetti non di tipo SDK.</span><span class="sxs-lookup"><span data-stu-id="08767-135">Migrated projects are not SDK-style projects.</span></span> |

## <a name="check-the-project-format"></a><span data-ttu-id="08767-136">Controllare il formato del progetto</span><span class="sxs-lookup"><span data-stu-id="08767-136">Check the project format</span></span>

<span data-ttu-id="08767-137">Se non si è certi che il progetto sia di tipo SDK o meno, cercare l'attributo SDK nell'elemento `<Project>` nel file di progetto (per C#, questo è il file con estensione csproj).</span><span class="sxs-lookup"><span data-stu-id="08767-137">If you're unsure whether the project is SDK-style format or not, look for the SDK attribute in the `<Project>` element in the project file (For C#, this is the \*.csproj file).</span></span> <span data-ttu-id="08767-138">Se è presente, il progetto è di tipo SDK.</span><span class="sxs-lookup"><span data-stu-id="08767-138">If it is present, the project is an SDK-style project.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a><span data-ttu-id="08767-139">Controllare il formato del progetto in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="08767-139">Check the project format in Visual Studio</span></span>

<span data-ttu-id="08767-140">Se si usa Visual Studio, è possibile verificare rapidamente il formato del progetto con uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="08767-140">If you are working in Visual Studio, you can quickly check the project format using one of the following methods:</span></span>

- <span data-ttu-id="08767-141">Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni e scegliere **Modifica nomeprogetto.csproj**.</span><span class="sxs-lookup"><span data-stu-id="08767-141">Right-click the project in Solution Explorer and select **Edit myprojectname.csproj**.</span></span>

   <span data-ttu-id="08767-142">Questa opzione è disponibile solo a partire da Visual Studio 2017 per i progetti che usano l'attributo SDK.</span><span class="sxs-lookup"><span data-stu-id="08767-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="08767-143">In caso contrario, usare l'altro metodo.</span><span class="sxs-lookup"><span data-stu-id="08767-143">Otherwise, use the other method.</span></span>

   ![Modificare il file di progetto](media/edit-project-file.png)

   <span data-ttu-id="08767-145">Un progetto di tipo SDK mostra l'[attributo SDK](/dotnet/core/tools/csproj#additions) nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="08767-145">An SDK-style project shows the [SDK attribute](/dotnet/core/tools/csproj#additions) in the project file.</span></span>
   
- <span data-ttu-id="08767-146">Scegliere **Scarica progetto** dal menu **Progetto** oppure fare clic con il pulsante destro del mouse sul progetto e scegliere **Scarica progetto**.</span><span class="sxs-lookup"><span data-stu-id="08767-146">From the **Project** menu, choose **Unload Project** (or right-click the project and choose **Unload Project**).</span></span>

   <span data-ttu-id="08767-147">Questo progetto non includerà l'attributo SDK nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="08767-147">This project will not include the SDK attribute in the project file.</span></span> <span data-ttu-id="08767-148">Non è un progetto di tipo SDK.</span><span class="sxs-lookup"><span data-stu-id="08767-148">It is not an SDK-style project.</span></span>

   ![Scaricare il progetto](media/unload-project.png)

   <span data-ttu-id="08767-150">Fare quindi clic con il pulsante destro del mouse sul progetto scaricato e scegliere **Modifica nomeprogetto.csproj**.</span><span class="sxs-lookup"><span data-stu-id="08767-150">Then, right-click the unloaded project and choose **Edit myprojectname.csproj**.</span></span>

## <a name="see-also"></a><span data-ttu-id="08767-151">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08767-151">See also</span></span>

- [<span data-ttu-id="08767-152">Creare pacchetti .NET Standard con l'interfaccia della riga di comando dotnet</span><span class="sxs-lookup"><span data-stu-id="08767-152">Create .NET Standard Packages with dotnet CLI</span></span>](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [<span data-ttu-id="08767-153">Creare pacchetti .NET Standard con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="08767-153">Create .NET Standard Packages with Visual Studio</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [<span data-ttu-id="08767-154">Creare e pubblicare un pacchetto .NET Framework (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="08767-154">Create and publish a .NET Framework package (Visual Studio)</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [<span data-ttu-id="08767-155">Pack e restore di NuGet come destinazioni MSBuild</span><span class="sxs-lookup"><span data-stu-id="08767-155">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
