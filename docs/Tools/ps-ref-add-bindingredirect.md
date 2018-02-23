---
title: Riferimento di PowerShell di NuGet BindingRedirect aggiungere | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando di PowerShell Add-BindingRedirect nella Console di gestione pacchetti NuGet in Visual Studio.
keywords: Console di gestione, i comandi di Powershell di NuGet, riferimento di Powershell di NuGet, Aggiungi BindingRedirect del pacchetto NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 41f27d7a1b6b363a562f26590b220d9e11e944f1
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="b02af-104">Aggiungere-BindingRedirect (Console di gestione dei pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="b02af-104">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="b02af-105">*Disponibile solo all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="b02af-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="b02af-106">Esamina tutti gli assembly nel percorso di output per un progetto e aggiunge reindirizzamenti di binding al file di configurazione dell'applicazione o web, se necessario.</span><span class="sxs-lookup"><span data-stu-id="b02af-106">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="b02af-107">Questo comando viene eseguito automaticamente quando si installa un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="b02af-107">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="b02af-108">Per informazioni dettagliate sull'associazione di reindirizzamenti e perché vengono usati, vedere [reindirizzamento delle versioni degli Assembly](/dotnet/framework/configure-apps/redirect-assembly-versions) nella documentazione di .NET.</span><span class="sxs-lookup"><span data-stu-id="b02af-108">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="b02af-109">Sintassi</span><span class="sxs-lookup"><span data-stu-id="b02af-109">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="b02af-110">Parametri</span><span class="sxs-lookup"><span data-stu-id="b02af-110">Parameters</span></span>

| <span data-ttu-id="b02af-111">Parametro</span><span class="sxs-lookup"><span data-stu-id="b02af-111">Parameter</span></span> | <span data-ttu-id="b02af-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b02af-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b02af-113">ProjectName</span><span class="sxs-lookup"><span data-stu-id="b02af-113">ProjectName</span></span> | <span data-ttu-id="b02af-114">(Obbligatorio) Il progetto a cui aggiungere reindirizzamenti di associazione.</span><span class="sxs-lookup"><span data-stu-id="b02af-114">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="b02af-115">L'opzione - ProjectName stesso è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="b02af-115">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="b02af-116">Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.</span><span class="sxs-lookup"><span data-stu-id="b02af-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="b02af-117">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="b02af-117">Common Parameters</span></span>

<span data-ttu-id="b02af-118">`Add-BindingRedirect` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b02af-118">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="b02af-119">Esempi</span><span class="sxs-lookup"><span data-stu-id="b02af-119">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```