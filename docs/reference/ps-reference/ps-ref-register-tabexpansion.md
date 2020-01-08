---
title: Registro NuGet-riferimenti PowerShell per TabExpansion
description: Riferimento per il comando Register-TabExpansion di PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 37aed96760e642b03c02bf31fe47a54f0e3cb74a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384454"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="ef29c-103">Register-TabExpansion (console di gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="ef29c-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ef29c-104">*Disponibile solo nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="ef29c-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="ef29c-105">Registra un'espansione di tabulazione per i parametri del comando specificato, in modo che quando si immette un comando si utilizza TAB, i valori espansi vengono visualizzati come opzioni disponibili per il parametro in questione.</span><span class="sxs-lookup"><span data-stu-id="ef29c-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="ef29c-106">Qualsiasi espansione precedente per il comando viene sovrascritta.</span><span class="sxs-lookup"><span data-stu-id="ef29c-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="ef29c-107">Sintassi</span><span class="sxs-lookup"><span data-stu-id="ef29c-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="ef29c-108">Parametri</span><span class="sxs-lookup"><span data-stu-id="ef29c-108">Parameters</span></span>

| <span data-ttu-id="ef29c-109">Parametro</span><span class="sxs-lookup"><span data-stu-id="ef29c-109">Parameter</span></span> | <span data-ttu-id="ef29c-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ef29c-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ef29c-111">Name</span><span class="sxs-lookup"><span data-stu-id="ef29c-111">Name</span></span> | <span data-ttu-id="ef29c-112">Necessaria Comando a cui registrare le espansioni.</span><span class="sxs-lookup"><span data-stu-id="ef29c-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="ef29c-113">L'opzione-Name è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="ef29c-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="ef29c-114">Definizione</span><span class="sxs-lookup"><span data-stu-id="ef29c-114">Definition</span></span> | <span data-ttu-id="ef29c-115">Necessaria Oggetto che descrive l'argomento nella sintassi `@{'<parameter>' = {'<value1>', '<value2>', ...}}` dove `<parameter>` è il nome del parametro da modificare e ogni `<value>` fornisce un'espansione specifica.</span><span class="sxs-lookup"><span data-stu-id="ef29c-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="ef29c-116">Vengono accettate le virgolette singole e doppie.</span><span class="sxs-lookup"><span data-stu-id="ef29c-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="ef29c-117">Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="ef29c-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ef29c-118">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="ef29c-118">Common Parameters</span></span>

<span data-ttu-id="ef29c-119">`Register-TabExpansion` supporta i [parametri di PowerShell comuni](https://go.microsoft.com/fwlink/?LinkID=113216)seguenti: debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="ef29c-119">`Register-TabExpansion` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ef29c-120">Esempi</span><span class="sxs-lookup"><span data-stu-id="ef29c-120">Examples</span></span>

<span data-ttu-id="ef29c-121">Si consideri una soluzione che contiene tre nomi di progetti EventManager, Utilities e SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="ef29c-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="ef29c-122">Lo sviluppatore usa spesso il comando `Update-Package` in momenti diversi con ognuno di questi progetti.</span><span class="sxs-lookup"><span data-stu-id="ef29c-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="ef29c-123">Trova la pratica di fare in modo che il comando `Update-Package` fornisca espansioni di completamento automatico per l'argomento `-ProjectName`, in modo che non sia necessario digitare ogni volta un nome di progetto.</span><span class="sxs-lookup"><span data-stu-id="ef29c-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="ef29c-124">Il comando seguente, quindi, registra questi tre nomi di progetto come un'espansione per il parametro `-ProjectName`:</span><span class="sxs-lookup"><span data-stu-id="ef29c-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="ef29c-125">Lo sviluppatore può quindi digitare `Update-Package -ProjectName `, premere TAB e visualizzare le espansioni offerte come opzioni di completamento automatico:</span><span class="sxs-lookup"><span data-stu-id="ef29c-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Esempio di uso di Register-TabExpansion](media/Register-TabExpansion-Example.png)
