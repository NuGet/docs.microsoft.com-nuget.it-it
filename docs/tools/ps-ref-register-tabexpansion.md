---
title: Riferimento di PowerShell Register-TabExpansion NuGet
description: Informazioni di riferimento per il comando di PowerShell Register-TabExpansion nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8adb80af85e2e32fa8c35e5272cf90ff0c0ddcbb
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842491"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="67bb4-103">Register-TabExpansion (Console di gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="67bb4-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="67bb4-104">*Disponibile solo all'interno di [Console di gestione pacchetti](package-manager-console.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="67bb4-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="67bb4-105">Registra un'espansione tramite tab per i parametri del comando specificato, in modo che quando scheda viene usata quando si immette un comando, i valori espansi vengono visualizzati come opzioni disponibili per il parametro in questione.</span><span class="sxs-lookup"><span data-stu-id="67bb4-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="67bb4-106">Qualsiasi espansioni precedente per il comando vengono sovrascritti.</span><span class="sxs-lookup"><span data-stu-id="67bb4-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="67bb4-107">Sintassi</span><span class="sxs-lookup"><span data-stu-id="67bb4-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="67bb4-108">Parametri</span><span class="sxs-lookup"><span data-stu-id="67bb4-108">Parameters</span></span>

| <span data-ttu-id="67bb4-109">Parametro</span><span class="sxs-lookup"><span data-stu-id="67bb4-109">Parameter</span></span> | <span data-ttu-id="67bb4-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="67bb4-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="67bb4-111">Name</span><span class="sxs-lookup"><span data-stu-id="67bb4-111">Name</span></span> | <span data-ttu-id="67bb4-112">(Obbligatorio) Il comando per cui si desidera registrare le espansioni.</span><span class="sxs-lookup"><span data-stu-id="67bb4-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="67bb4-113">-Nome commutatore stesso è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="67bb4-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="67bb4-114">Definizione</span><span class="sxs-lookup"><span data-stu-id="67bb4-114">Definition</span></span> | <span data-ttu-id="67bb4-115">(Obbligatorio) Oggetto che descrive l'argomento nella sintassi `@{'<parameter>' = {'<value1>', '<value2>', ...}}` in cui `<parameter>` è il nome del parametro da modificare e ogni `<value>` fornisce un'espansione specifica.</span><span class="sxs-lookup"><span data-stu-id="67bb4-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="67bb4-116">Le virgolette singole e doppie sono accettate.</span><span class="sxs-lookup"><span data-stu-id="67bb4-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="67bb4-117">Nessuno di questi parametri accettano caratteri jolly o input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="67bb4-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="67bb4-118">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="67bb4-118">Common Parameters</span></span>

<span data-ttu-id="67bb4-119">`Register-TabExpansion` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione per errore, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="67bb4-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="67bb4-120">Esempi</span><span class="sxs-lookup"><span data-stu-id="67bb4-120">Examples</span></span>

<span data-ttu-id="67bb4-121">Prendere in considerazione una soluzione che contiene tre nomi di progetti EventManager, utilità e SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="67bb4-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="67bb4-122">Lo sviluppatore utilizza spesso il `Update-Package` comando in momenti diversi con ciascuno di questi progetti.</span><span class="sxs-lookup"><span data-stu-id="67bb4-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="67bb4-123">Anna risulta utile avere la `Update-Package` comandi forniscono le espansioni di completamento automatico per il `-ProjectName` argomento in modo che non sono necessari per digitare un nome di progetto ogni volta.</span><span class="sxs-lookup"><span data-stu-id="67bb4-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="67bb4-124">Il comando seguente, quindi Registra i nomi di tre progetti come un'espansione per il `-ProjectName` parametro:</span><span class="sxs-lookup"><span data-stu-id="67bb4-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="67bb4-125">Lo sviluppatore può quindi digitare `Update-Package -ProjectName `, premere Tab e vedere le espansioni presentate come scelte di completamento automatico:</span><span class="sxs-lookup"><span data-stu-id="67bb4-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Esempio dell'uso di Register-TabExpansion](media/Register-TabExpansion-Example.png)
