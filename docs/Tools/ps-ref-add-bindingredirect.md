---
title: Riferimento di PowerShell di NuGet BindingRedirect aggiungere | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 90f4dcb0-6e5a-4948-8ea9-62e0d061d95a
description: Riferimento per il comando di PowerShell Add-BindingRedirect nella Console di gestione pacchetti NuGet in Visual Studio.
keywords: Console di gestione, i comandi di Powershell di NuGet, riferimento di Powershell di NuGet, Aggiungi BindingRedirect del pacchetto NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7bf8cdb938195f4747932b38ef0d5bb6c34b9137
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="77b6e-104">Aggiungere-BindingRedirect (Console di gestione dei pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="77b6e-104">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="77b6e-105">*Disponibile solo all'interno di [Console di gestione pacchetti NuGet](Package-Manager-Console.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="77b6e-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="77b6e-106">Esamina tutti gli assembly nel percorso di output per un progetto e aggiunge reindirizzamenti di binding al file di configurazione dell'applicazione o web, se necessario.</span><span class="sxs-lookup"><span data-stu-id="77b6e-106">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="77b6e-107">Questo comando viene eseguito automaticamente quando si installa un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="77b6e-107">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="77b6e-108">Per informazioni dettagliate sull'associazione di reindirizzamenti e perché vengono usati, vedere [reindirizzamento delle versioni degli Assembly](https://docs.microsoft.com/dotnet/framework/configure-apps/redirect-assembly-versions) nella documentazione di .NET.</span><span class="sxs-lookup"><span data-stu-id="77b6e-108">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](https://docs.microsoft.com/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="77b6e-109">Sintassi</span><span class="sxs-lookup"><span data-stu-id="77b6e-109">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="77b6e-110">Parametri</span><span class="sxs-lookup"><span data-stu-id="77b6e-110">Parameters</span></span>

| <span data-ttu-id="77b6e-111">Parametro</span><span class="sxs-lookup"><span data-stu-id="77b6e-111">Parameter</span></span> | <span data-ttu-id="77b6e-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="77b6e-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="77b6e-113">ProjectName</span><span class="sxs-lookup"><span data-stu-id="77b6e-113">ProjectName</span></span> | <span data-ttu-id="77b6e-114">(Obbligatorio) Il progetto a cui aggiungere reindirizzamenti di associazione.</span><span class="sxs-lookup"><span data-stu-id="77b6e-114">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="77b6e-115">L'opzione - ProjectName stesso è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="77b6e-115">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="77b6e-116">Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.</span><span class="sxs-lookup"><span data-stu-id="77b6e-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="77b6e-117">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="77b6e-117">Common Parameters</span></span>

<span data-ttu-id="77b6e-118">`Add-BindingRedirect`supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="77b6e-118">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="77b6e-119">Esempi</span><span class="sxs-lookup"><span data-stu-id="77b6e-119">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```