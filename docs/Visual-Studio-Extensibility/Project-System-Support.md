---
title: Supporto di NuGet per il sistema di progetto di Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 9d7fa7f6-82ed-4df6-9734-f43a3d8e3b98
description: Integrazione di NuGet nel sistema di progetto in Visual Studio per i tipi di progetto di terze parti.
keywords: NuGet in Visual Studio, tipi di progetto personalizzati, progetti di Visual Studio
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 39212361e7cb2c214c3e83cef604d40cd057fd7e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="219af-104">Supporto di NuGet per il sistema di progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="219af-104">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="219af-105">Per supportare i tipi di progetto di terze parti in Visual Studio, NuGet 3.x+ supporta [CPS (Common Project System)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md) e NuGet 3.2+ supporta anche i sistemi di progetto non CPS.</span><span class="sxs-lookup"><span data-stu-id="219af-105">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="219af-106">Per integrarsi con NuGet, un sistema di progetto deve annunciare il proprio supporto per tutte le funzionalità del progetto descritte in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="219af-106">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>


> [!NOTE]
> <span data-ttu-id="219af-107">Non dichiarare funzionalità non effettivamente disponibili nel progetto per consentire l'installazione dei pacchetti nel progetto.</span><span class="sxs-lookup"><span data-stu-id="219af-107">Do not declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="219af-108">Diverse funzionalità di Visual Studio e di altre estensioni dipendono da funzionalità del progetto al di fuori del client NuGet.</span><span class="sxs-lookup"><span data-stu-id="219af-108">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="219af-109">L'annuncio di funzionalità del progetto non effettivamente disponibili può causare il malfunzionamento di questi componenti e il peggioramento dell'esperienza degli utenti.</span><span class="sxs-lookup"><span data-stu-id="219af-109">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="219af-110">Annunciare le funzionalità del progetto</span><span class="sxs-lookup"><span data-stu-id="219af-110">Advertise project capabilities</span></span>

<span data-ttu-id="219af-111">Il client NuGet determina quali pacchetti sono compatibili con il tipo di progetto in base alle [funzionalità del progetto](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), come illustrato nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="219af-111">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>


|<span data-ttu-id="219af-112">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="219af-112">Capability</span></span>|<span data-ttu-id="219af-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="219af-113">Description</span></span>|
|----------------|-----------|
|<span data-ttu-id="219af-114">AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="219af-114">AssemblyReferences</span></span>|<span data-ttu-id="219af-115">Indica che il progetto supporta i riferimenti ad assembly (diversi da WinRTReferences)</span><span class="sxs-lookup"><span data-stu-id="219af-115">Indicates that the project supports assembly references (distinct from WinRTReferences)</span></span>|
|<span data-ttu-id="219af-116">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="219af-116">DeclaredSourceItems</span></span>|<span data-ttu-id="219af-117">Indica che il progetto è un tipico progetto MSBuild (non DNX) che dichiara gli elementi di origine nel progetto stesso (invece che in un file `project.json` che presuppone che tutti i file nella cartella facciano parte di una compilazione).</span><span class="sxs-lookup"><span data-stu-id="219af-117">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself (rather than a `project.json` file that assumes all files in the folder are part of a compilation).</span></span>|
|<span data-ttu-id="219af-118">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="219af-118">UserSourceItems</span></span>|<span data-ttu-id="219af-119">Indica che all'utente è consentito aggiungere file arbitrari al progetto.</span><span class="sxs-lookup"><span data-stu-id="219af-119">Indicates that the user is allowed to add arbitrary files to their project.</span></span>|

<span data-ttu-id="219af-120">Per i sistemi di progetto basati su CPS, l'implementazione dettagliata delle funzionalità del progetto descritte nella parte restante di questa sezione è stata eseguita automaticamente.</span><span class="sxs-lookup"><span data-stu-id="219af-120">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="219af-121">Vedere [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project) (Dichiarazione delle funzionalità del progetto nei progetti CPS).</span><span class="sxs-lookup"><span data-stu-id="219af-121">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="219af-122">Implementazione di VsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="219af-122">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="219af-123">La classe `VsProjectCapabilitiesPresenceChecker` deve implementare l'interfaccia `IVsBooleanSymbolPresenceChecker`, definita come segue:</span><span class="sxs-lookup"><span data-stu-id="219af-123">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

```cs
public interface IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// Checks whether the symbols defined may have changed since the last time
    /// this method was called.
    /// </summary>
    /// <param name="versionObject">
    /// The response version object assigned at the last call.
    /// May be null to get the initial version.
    /// At the conclusion of this method call, the reference may be changed so that on a subsequent call
    /// we know what version was last observed. The caller should treat this value as an opaque object,
    /// and should not assume any significance from whether the pointer changed or not.
    /// </param>
    /// <returns>
    /// <c>true</c> if the symbols defined may have changed since the last call to this method
    /// or if <paramref name="versionObject"/> was <c>null</c> upon entering this method.
    /// <c>false</c> if the responses would all be the same.
    /// </returns>
    bool HasChangedSince(ref object versionObject);

    /// <summary>
    /// Checks for the presence of a given symbol.
    /// </summary>
    /// <param name="symbol">The symbol to check for.</param>
    /// <returns><c>true</c> if the symbol is present; <c>false</c> otherwise.</returns>
    bool IsSymbolPresent(string symbol);
}
```


<span data-ttu-id="219af-124">Un'implementazione di esempio di questa interfaccia sarebbe quindi:</span><span class="sxs-lookup"><span data-stu-id="219af-124">A sample implementation of this interface would then be:</span></span>
    
```cs
class VsProjectCapabilitiesPresenceChecker : IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// The set of capabilities this project system actually has.
    /// This should be kept current, and honestly reflect what the project can do.
    /// </summary>
    private static readonly HashSet<string> ActualProjectCapabilities = new HashSet<string>(StringComparer.OrdinalIgnoreCase)
        {
            "AssemblyReferences",
            "DeclaredSourceItems",
            "UserSourceItems",
        };

    public bool HasChangedSince(ref object versionObject)
    {
        // If your project capabilities do not change over time while the project is open,
        // you may simply `return false;` from your `HasChangedSince` method.
        return false;
    }

    public bool IsSymbolPresent(string symbol)
    {
        return ActualProjectCapabilities.Contains(symbol);
    }
}
```

<span data-ttu-id="219af-125">Si ricordi di aggiungere/rimuovere le funzionalità dal set `ActualProjectCapabilities` a seconda di quelle effettivamente supportate dal sistema.</span><span class="sxs-lookup"><span data-stu-id="219af-125">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="219af-126">Per le descrizioni complete, vedere la [documentazione delle funzionalità del progetto](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="219af-126">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="219af-127">Risposta alle query</span><span class="sxs-lookup"><span data-stu-id="219af-127">Responding to queries</span></span>

<span data-ttu-id="219af-128">Un progetto dichiara questa funzionalità supportando la proprietà `VSHPROPID_ProjectCapabilitiesChecker` tramite `IVsHierarchy::GetProperty`.</span><span class="sxs-lookup"><span data-stu-id="219af-128">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="219af-129">Deve restituire un'istanza di `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, definita nell'assembly `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll`.</span><span class="sxs-lookup"><span data-stu-id="219af-129">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="219af-130">Per fare riferimento a questo assembly, installare il [pacchetto NuGet specifico](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span><span class="sxs-lookup"><span data-stu-id="219af-130">Reference this assembly by installing the [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="219af-131">È ad esempio possibile aggiungere l'istruzione `case` seguente all'istruzione `switch` del metodo `IVsHierarchy::GetProperty`:</span><span class="sxs-lookup"><span data-stu-id="219af-131">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```


## <a name="dte-support"></a><span data-ttu-id="219af-132">Supporto DTE</span><span class="sxs-lookup"><span data-stu-id="219af-132">DTE Support</span></span>

<span data-ttu-id="219af-133">NuGet consente al sistema di progetto di aggiungere riferimenti, elementi di contenuto e importazioni MSBuild chiamando [DTE](https://msdn.microsoft.com/library/mt452175.aspx), ovvero l'interfaccia di automazione principale di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="219af-133">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](https://msdn.microsoft.com/library/mt452175.aspx), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="219af-134">DTE è un set di interfacce COM che è già possibile implementare.</span><span class="sxs-lookup"><span data-stu-id="219af-134">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="219af-135">Se il tipo di progetto è basato su CPS, DTE viene implementato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="219af-135">If your project type is based on CPS, DTE is implemented for you.</span></span>
