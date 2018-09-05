---
title: Informazioni di riferimento di NuGet aggiungere-BindingRedirect PowerShell
description: Informazioni di riferimento per il comando di PowerShell Add-BindingRedirect nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: dec7db04c5cf239863b9c00e9f5bc0dde42c7e47
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551657"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="394bf-103">Add-BindingRedirect (console di Gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="394bf-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="394bf-104">*Disponibile solo all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="394bf-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="394bf-105">Esamina tutti gli assembly all'interno del percorso di output per un progetto e aggiunge reindirizzamenti di binding al file di configurazione dell'applicazione o web dove necessario.</span><span class="sxs-lookup"><span data-stu-id="394bf-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="394bf-106">Questo comando viene eseguito automaticamente quando si installa un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="394bf-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="394bf-107">Per informazioni dettagliate sull'associazione di reindirizzamenti e il motivo per cui vengono usati, vedere [reindirizzamento delle versioni degli Assembly](/dotnet/framework/configure-apps/redirect-assembly-versions) nella documentazione di .NET.</span><span class="sxs-lookup"><span data-stu-id="394bf-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="394bf-108">Sintassi</span><span class="sxs-lookup"><span data-stu-id="394bf-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="394bf-109">Parametri</span><span class="sxs-lookup"><span data-stu-id="394bf-109">Parameters</span></span>

| <span data-ttu-id="394bf-110">Parametro</span><span class="sxs-lookup"><span data-stu-id="394bf-110">Parameter</span></span> | <span data-ttu-id="394bf-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="394bf-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="394bf-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="394bf-112">ProjectName</span></span> | <span data-ttu-id="394bf-113">(Obbligatorio) Il progetto a cui aggiungere reindirizzamenti di associazione.</span><span class="sxs-lookup"><span data-stu-id="394bf-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="394bf-114">L'opzione - nomeprogetto è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="394bf-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="394bf-115">Nessuno di questi parametri accettano caratteri jolly o input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="394bf-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="394bf-116">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="394bf-116">Common Parameters</span></span>

<span data-ttu-id="394bf-117">`Add-BindingRedirect` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione per errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="394bf-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="394bf-118">Esempi</span><span class="sxs-lookup"><span data-stu-id="394bf-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```