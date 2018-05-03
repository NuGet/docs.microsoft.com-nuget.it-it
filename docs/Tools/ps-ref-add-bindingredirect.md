---
title: Riferimento di PowerShell aggiungere BindingRedirect NuGet
description: Riferimento per il comando di PowerShell Add-BindingRedirect nella Console di gestione pacchetti NuGet in Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7f1f2ef23e54ee48b577a2796b7f7b5f4c7eb284
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="b1767-103">Aggiungere-BindingRedirect (Console di gestione dei pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="b1767-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="b1767-104">*Disponibile solo all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="b1767-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="b1767-105">Esamina tutti gli assembly nel percorso di output per un progetto e aggiunge reindirizzamenti di binding al file di configurazione dell'applicazione o web, se necessario.</span><span class="sxs-lookup"><span data-stu-id="b1767-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="b1767-106">Questo comando viene eseguito automaticamente quando si installa un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="b1767-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="b1767-107">Per informazioni dettagliate sull'associazione di reindirizzamenti e perché vengono usati, vedere [reindirizzamento delle versioni degli Assembly](/dotnet/framework/configure-apps/redirect-assembly-versions) nella documentazione di .NET.</span><span class="sxs-lookup"><span data-stu-id="b1767-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="b1767-108">Sintassi</span><span class="sxs-lookup"><span data-stu-id="b1767-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="b1767-109">Parametri</span><span class="sxs-lookup"><span data-stu-id="b1767-109">Parameters</span></span>

| <span data-ttu-id="b1767-110">Parametro</span><span class="sxs-lookup"><span data-stu-id="b1767-110">Parameter</span></span> | <span data-ttu-id="b1767-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b1767-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b1767-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="b1767-112">ProjectName</span></span> | <span data-ttu-id="b1767-113">(Obbligatorio) Il progetto a cui aggiungere reindirizzamenti di associazione.</span><span class="sxs-lookup"><span data-stu-id="b1767-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="b1767-114">L'opzione - ProjectName stesso è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="b1767-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="b1767-115">Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.</span><span class="sxs-lookup"><span data-stu-id="b1767-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="b1767-116">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="b1767-116">Common Parameters</span></span>

<span data-ttu-id="b1767-117">`Add-BindingRedirect` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b1767-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="b1767-118">Esempi</span><span class="sxs-lookup"><span data-stu-id="b1767-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```