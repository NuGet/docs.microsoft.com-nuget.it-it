---
title: Registro NuGet-riferimenti PowerShell per TabExpansion
description: Riferimento per il comando Register-TabExpansion di PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 14cda695677e1052c78169fda097b72b460a9d43
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327298"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="9a1de-103">Register-TabExpansion (console di gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="9a1de-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="9a1de-104">*Disponibile solo nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="9a1de-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="9a1de-105">Registra un'espansione di tabulazione per i parametri del comando specificato, in modo che quando si immette un comando si utilizza TAB, i valori espansi vengono visualizzati come opzioni disponibili per il parametro in questione.</span><span class="sxs-lookup"><span data-stu-id="9a1de-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="9a1de-106">Qualsiasi espansione precedente per il comando viene sovrascritta.</span><span class="sxs-lookup"><span data-stu-id="9a1de-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="9a1de-107">Sintassi</span><span class="sxs-lookup"><span data-stu-id="9a1de-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="9a1de-108">Parametri</span><span class="sxs-lookup"><span data-stu-id="9a1de-108">Parameters</span></span>

| <span data-ttu-id="9a1de-109">Parametro</span><span class="sxs-lookup"><span data-stu-id="9a1de-109">Parameter</span></span> | <span data-ttu-id="9a1de-110">DESCRIZIONE</span><span class="sxs-lookup"><span data-stu-id="9a1de-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9a1de-111">Name</span><span class="sxs-lookup"><span data-stu-id="9a1de-111">Name</span></span> | <span data-ttu-id="9a1de-112">Necessaria Comando a cui registrare le espansioni.</span><span class="sxs-lookup"><span data-stu-id="9a1de-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="9a1de-113">L'opzione-Name è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="9a1de-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="9a1de-114">Definizione</span><span class="sxs-lookup"><span data-stu-id="9a1de-114">Definition</span></span> | <span data-ttu-id="9a1de-115">Necessaria Oggetto che descrive l'argomento nella sintassi `@{'<parameter>' = {'<value1>', '<value2>', ...}}` in cui `<parameter>` è il nome del parametro da modificare e ognuno `<value>` fornisce un'espansione specifica.</span><span class="sxs-lookup"><span data-stu-id="9a1de-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="9a1de-116">Vengono accettate le virgolette singole e doppie.</span><span class="sxs-lookup"><span data-stu-id="9a1de-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="9a1de-117">Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="9a1de-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="9a1de-118">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="9a1de-118">Common Parameters</span></span>

<span data-ttu-id="9a1de-119">`Register-TabExpansion`supporta i seguenti [parametri comuni di PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9a1de-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="9a1de-120">Esempi</span><span class="sxs-lookup"><span data-stu-id="9a1de-120">Examples</span></span>

<span data-ttu-id="9a1de-121">Si consideri una soluzione che contiene tre nomi di progetti EventManager, Utilities e SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="9a1de-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="9a1de-122">Lo sviluppatore usa spesso il `Update-Package` comando in momenti diversi con ognuno di questi progetti.</span><span class="sxs-lookup"><span data-stu-id="9a1de-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="9a1de-123">Trova praticità che il `Update-Package` comando fornisca espansioni di completamento automatico per l' `-ProjectName` argomento in modo che non debba digitare ogni volta un nome di progetto.</span><span class="sxs-lookup"><span data-stu-id="9a1de-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="9a1de-124">Il comando seguente, quindi, registra questi tre nomi di progetto come un'espansione per `-ProjectName` il parametro:</span><span class="sxs-lookup"><span data-stu-id="9a1de-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="9a1de-125">Lo sviluppatore può quindi digitare `Update-Package -ProjectName `, premere TAB e visualizzare le espansioni offerte come opzioni di completamento automatico:</span><span class="sxs-lookup"><span data-stu-id="9a1de-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Esempio di uso di Register-TabExpansion](media/Register-TabExpansion-Example.png)
