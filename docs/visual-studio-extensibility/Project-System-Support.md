---
title: Supporto di NuGet per il sistema di progetto di Visual Studio
description: Integrazione di NuGet nel sistema di progetto in Visual Studio per i tipi di progetto di terze parti.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 7af330f88b47352666933598719d9c8f8cb66a78
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779401"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Supporto di NuGet per il sistema di progetto di Visual Studio

Per supportare i tipi di progetto di terze parti in Visual Studio, NuGet 3.x+ supporta [CPS (Common Project System)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md) e NuGet 3.2+ supporta anche i sistemi di progetto non CPS.

Per integrarsi con NuGet, un sistema di progetto deve annunciare il proprio supporto per tutte le funzionalità del progetto descritte in questo argomento.

> [!Note]
> Non dichiarare funzionalità non effettivamente disponibili nel progetto per consentire l'installazione dei pacchetti nel progetto. Diverse funzionalità di Visual Studio e di altre estensioni dipendono da funzionalità del progetto al di fuori del client NuGet. L'annuncio di funzionalità del progetto non effettivamente disponibili può causare il malfunzionamento di questi componenti e il peggioramento dell'esperienza degli utenti.

## <a name="advertise-project-capabilities"></a>Annunciare le funzionalità del progetto

Il client NuGet determina quali pacchetti sono compatibili con il tipo di progetto in base alle [funzionalità del progetto](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), come illustrato nella tabella seguente.

| Funzionalità | Descrizione |
| --- | --- |
| AssemblyReferences | Indica che il progetto supporta i riferimenti ad assembly (diversi da WinRTReferences). |
| DeclaredSourceItems | Indica che il progetto è un tipico progetto MSBuild (non DNX), ovvero contiene la dichiarazione degli elementi di origine nel progetto stesso. |
| UserSourceItems|Indica che all'utente è consentito aggiungere file arbitrari al progetto. |

Per i sistemi di progetto basati su CPS, l'implementazione dettagliata delle funzionalità del progetto descritte nella parte restante di questa sezione è stata eseguita automaticamente. Vedere [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project) (Dichiarazione delle funzionalità del progetto nei progetti CPS).

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>Implementazione di VsProjectCapabilitiesPresenceChecker

La classe `VsProjectCapabilitiesPresenceChecker` deve implementare l'interfaccia `IVsBooleanSymbolPresenceChecker`, definita come segue:

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

Un'implementazione di esempio di questa interfaccia sarebbe quindi:

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

Si ricordi di aggiungere/rimuovere le funzionalità dal set `ActualProjectCapabilities` a seconda di quelle effettivamente supportate dal sistema. Per le descrizioni complete, vedere la [documentazione delle funzionalità del progetto](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md).

## <a name="responding-to-queries"></a>Risposta alle query

Un progetto dichiara questa funzionalità supportando la proprietà `VSHPROPID_ProjectCapabilitiesChecker` tramite `IVsHierarchy::GetProperty`. Deve restituire un'istanza di `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, definita nell'assembly `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll`. Per fare riferimento a questo assembly, installare il [pacchetto NuGet corrispondente](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).

È ad esempio possibile aggiungere l'istruzione `case` seguente all'istruzione `switch` del metodo `IVsHierarchy::GetProperty`:

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>Supporto DTE

NuGet consente al sistema di progetto di aggiungere riferimenti, elementi di contenuto e importazioni MSBuild chiamando [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), ovvero l'interfaccia di automazione principale di Visual Studio. DTE è un set di interfacce COM che è già possibile implementare.

Se il tipo di progetto è basato su CPS, DTE viene implementato automaticamente.
