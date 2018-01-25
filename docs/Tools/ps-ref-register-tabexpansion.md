---
title: Riferimento di PowerShell di NuGet. Register-TabExpansion | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando Register-TabExpansion PowerShell nella Console di gestione pacchetti NuGet in Visual Studio.
keywords: Console di gestione, i comandi di Powershell di NuGet, riferimento di Powershell di NuGet, Register-TabExpansion del pacchetto NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5691c07f9efef4bfd12680421f3b02c5a523eb6f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="65504-104">Register-TabExpansion (Console di gestione dei pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="65504-104">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="65504-105">*Disponibile solo all'interno di [Console di gestione pacchetti NuGet](Package-Manager-Console.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="65504-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="65504-106">Registra l'espansione tramite tab per i parametri del comando specificato, in modo che quando scheda viene usata quando si immette un comando, i valori espansi vengono visualizzati come opzioni disponibili per il parametro in questione.</span><span class="sxs-lookup"><span data-stu-id="65504-106">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="65504-107">Qualsiasi espansioni precedente per il comando vengono sovrascritti.</span><span class="sxs-lookup"><span data-stu-id="65504-107">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="65504-108">Sintassi</span><span class="sxs-lookup"><span data-stu-id="65504-108">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="65504-109">Parametri</span><span class="sxs-lookup"><span data-stu-id="65504-109">Parameters</span></span>

| <span data-ttu-id="65504-110">Parametro</span><span class="sxs-lookup"><span data-stu-id="65504-110">Parameter</span></span> | <span data-ttu-id="65504-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="65504-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="65504-112">nome</span><span class="sxs-lookup"><span data-stu-id="65504-112">Name</span></span> | <span data-ttu-id="65504-113">(Obbligatorio) Il comando in cui registrare le espansioni.</span><span class="sxs-lookup"><span data-stu-id="65504-113">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="65504-114">-Nome switch stesso è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="65504-114">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="65504-115">Definizione</span><span class="sxs-lookup"><span data-stu-id="65504-115">Definition</span></span> | <span data-ttu-id="65504-116">(Obbligatorio) Oggetto che descrive l'argomento nella sintassi `@{'<parameter>' = {'<value1>', '<value2>', ...}}` in `<parameter>` è il nome del parametro da modificare e ogni `<value>` fornisce una specifica espansione.</span><span class="sxs-lookup"><span data-stu-id="65504-116">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="65504-117">Le virgolette singole e doppie vengono accettate.</span><span class="sxs-lookup"><span data-stu-id="65504-117">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="65504-118">Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.</span><span class="sxs-lookup"><span data-stu-id="65504-118">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="65504-119">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="65504-119">Common Parameters</span></span>

<span data-ttu-id="65504-120">`Register-TabExpansion`supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="65504-120">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="65504-121">Esempi</span><span class="sxs-lookup"><span data-stu-id="65504-121">Examples</span></span>

<span data-ttu-id="65504-122">Prendere in considerazione una soluzione che contiene tre nomi di progetti EventManager, utilità e SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="65504-122">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="65504-123">Lo sviluppatore utilizza spesso il `Update-Package` comando in momenti diversi, ognuno di questi progetti.</span><span class="sxs-lookup"><span data-stu-id="65504-123">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="65504-124">Individua consigliabile utilizzare il `Update-Package` comando forniscono le espansioni di completamento automatico per il `-ProjectName` argomento, quindi non necessita di digitare un nome di progetto ogni volta.</span><span class="sxs-lookup"><span data-stu-id="65504-124">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="65504-125">Il comando seguente, quindi Registra i nomi di tre progetti come un'espansione per le `-ProjectName` parametro:</span><span class="sxs-lookup"><span data-stu-id="65504-125">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="65504-126">Lo sviluppatore può quindi digitare `Update-Package -ProjectName `, premere il tasto Tab e vedere le espansioni presentate come scelte di completamento automatico:</span><span class="sxs-lookup"><span data-stu-id="65504-126">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Esempio di utilizzo registro TabExpansion](media/Register-TabExpansion-Example.png)
