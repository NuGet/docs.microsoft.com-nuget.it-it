---
title: Supporto di NuGet per il sistema di progetto di Visual Studio
description: Integrazione di NuGet nel sistema di progetto in Visual Studio per i tipi di progetto di terze parti.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: a9dd503c4c76adda6255d398cc400eb622721912
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="8fc44-103">Supporto di NuGet per il sistema di progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8fc44-103">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="8fc44-104">Per supportare i tipi di progetto di terze parti in Visual Studio, NuGet 3.x+ supporta [CPS (Common Project System)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md) e NuGet 3.2+ supporta anche i sistemi di progetto non CPS.</span><span class="sxs-lookup"><span data-stu-id="8fc44-104">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="8fc44-105">Per integrarsi con NuGet, un sistema di progetto deve annunciare il proprio supporto per tutte le funzionalità del progetto descritte in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="8fc44-105">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>

> [!Note]
> <span data-ttu-id="8fc44-106">Non dichiarare funzionalità non effettivamente disponibili nel progetto per consentire l'installazione dei pacchetti nel progetto.</span><span class="sxs-lookup"><span data-stu-id="8fc44-106">Don't declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="8fc44-107">Diverse funzionalità di Visual Studio e di altre estensioni dipendono da funzionalità del progetto al di fuori del client NuGet.</span><span class="sxs-lookup"><span data-stu-id="8fc44-107">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="8fc44-108">L'annuncio di funzionalità del progetto non effettivamente disponibili può causare il malfunzionamento di questi componenti e il peggioramento dell'esperienza degli utenti.</span><span class="sxs-lookup"><span data-stu-id="8fc44-108">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="8fc44-109">Annunciare le funzionalità del progetto</span><span class="sxs-lookup"><span data-stu-id="8fc44-109">Advertise project capabilities</span></span>

<span data-ttu-id="8fc44-110">Il client NuGet determina quali pacchetti sono compatibili con il tipo di progetto in base alle [funzionalità del progetto](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), come illustrato nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="8fc44-110">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>

| <span data-ttu-id="8fc44-111">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="8fc44-111">Capability</span></span> | <span data-ttu-id="8fc44-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8fc44-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8fc44-113">AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="8fc44-113">AssemblyReferences</span></span> | <span data-ttu-id="8fc44-114">Indica che il progetto supporta i riferimenti ad assembly (diversi da WinRTReferences).</span><span class="sxs-lookup"><span data-stu-id="8fc44-114">Indicates that the project supports assembly references (distinct from WinRTReferences).</span></span> |
| <span data-ttu-id="8fc44-115">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="8fc44-115">DeclaredSourceItems</span></span> | <span data-ttu-id="8fc44-116">Indica che il progetto è un tipico progetto MSBuild (non DNX), ovvero contiene la dichiarazione degli elementi di origine nel progetto stesso.</span><span class="sxs-lookup"><span data-stu-id="8fc44-116">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself.</span></span> |
| <span data-ttu-id="8fc44-117">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="8fc44-117">UserSourceItems</span></span>|<span data-ttu-id="8fc44-118">Indica che all'utente è consentito aggiungere file arbitrari al progetto.</span><span class="sxs-lookup"><span data-stu-id="8fc44-118">Indicates that the user is allowed to add arbitrary files to their project.</span></span> |

<span data-ttu-id="8fc44-119">Per i sistemi di progetto basati su CPS, l'implementazione dettagliata delle funzionalità del progetto descritte nella parte restante di questa sezione è stata eseguita automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8fc44-119">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="8fc44-120">Vedere [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project) (Dichiarazione delle funzionalità del progetto nei progetti CPS).</span><span class="sxs-lookup"><span data-stu-id="8fc44-120">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="8fc44-121">Implementazione di VsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="8fc44-121">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="8fc44-122">La classe `VsProjectCapabilitiesPresenceChecker` deve implementare l'interfaccia `IVsBooleanSymbolPresenceChecker`, definita come segue:</span><span class="sxs-lookup"><span data-stu-id="8fc44-122">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

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

<span data-ttu-id="8fc44-123">Un'implementazione di esempio di questa interfaccia sarebbe quindi:</span><span class="sxs-lookup"><span data-stu-id="8fc44-123">A sample implementation of this interface would then be:</span></span>

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

<span data-ttu-id="8fc44-124">Si ricordi di aggiungere/rimuovere le funzionalità dal set `ActualProjectCapabilities` a seconda di quelle effettivamente supportate dal sistema.</span><span class="sxs-lookup"><span data-stu-id="8fc44-124">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="8fc44-125">Per le descrizioni complete, vedere la [documentazione delle funzionalità del progetto](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="8fc44-125">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="8fc44-126">Risposta alle query</span><span class="sxs-lookup"><span data-stu-id="8fc44-126">Responding to queries</span></span>

<span data-ttu-id="8fc44-127">Un progetto dichiara questa funzionalità supportando la proprietà `VSHPROPID_ProjectCapabilitiesChecker` tramite `IVsHierarchy::GetProperty`.</span><span class="sxs-lookup"><span data-stu-id="8fc44-127">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="8fc44-128">Deve restituire un'istanza di `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, definita nell'assembly `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll`.</span><span class="sxs-lookup"><span data-stu-id="8fc44-128">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="8fc44-129">Per fare riferimento a questo assembly, installare il [pacchetto NuGet corrispondente](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span><span class="sxs-lookup"><span data-stu-id="8fc44-129">Reference this assembly by installing [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="8fc44-130">È ad esempio possibile aggiungere l'istruzione `case` seguente all'istruzione `switch` del metodo `IVsHierarchy::GetProperty`:</span><span class="sxs-lookup"><span data-stu-id="8fc44-130">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="8fc44-131">Supporto DTE</span><span class="sxs-lookup"><span data-stu-id="8fc44-131">DTE Support</span></span>

<span data-ttu-id="8fc44-132">NuGet consente al sistema di progetto di aggiungere riferimenti, elementi di contenuto e importazioni MSBuild chiamando [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), ovvero l'interfaccia di automazione principale di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8fc44-132">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="8fc44-133">DTE è un set di interfacce COM che è già possibile implementare.</span><span class="sxs-lookup"><span data-stu-id="8fc44-133">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="8fc44-134">Se il tipo di progetto è basato su CPS, DTE viene implementato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8fc44-134">If your project type is based on CPS, DTE is implemented for you.</span></span>
