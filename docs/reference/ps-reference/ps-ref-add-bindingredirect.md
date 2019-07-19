---
title: Riferimenti per PowerShell Add-BindingRedirect di NuGet
description: Informazioni di riferimento per il comando Add-BindingRedirect di PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b1e88d32deb3ff34833ef22a9cbb8cad3f0d4354
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327458"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="91600-103">Add-BindingRedirect (console di Gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="91600-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="91600-104">*Disponibile solo nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="91600-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="91600-105">Esamina tutti gli assembly nel percorso di output di un progetto e aggiunge i reindirizzamenti di associazione al file di configurazione dell'applicazione o del Web, ove necessario.</span><span class="sxs-lookup"><span data-stu-id="91600-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="91600-106">Questo comando viene eseguito automaticamente durante l'installazione di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="91600-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="91600-107">Per informazioni dettagliate sui reindirizzamenti di binding e sul motivo per cui vengono usati, vedere [Reindirizzamento delle versioni degli assembly](/dotnet/framework/configure-apps/redirect-assembly-versions) nella documentazione di .NET.</span><span class="sxs-lookup"><span data-stu-id="91600-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="91600-108">Sintassi</span><span class="sxs-lookup"><span data-stu-id="91600-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="91600-109">Parametri</span><span class="sxs-lookup"><span data-stu-id="91600-109">Parameters</span></span>

| <span data-ttu-id="91600-110">Parametro</span><span class="sxs-lookup"><span data-stu-id="91600-110">Parameter</span></span> | <span data-ttu-id="91600-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="91600-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="91600-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="91600-112">ProjectName</span></span> | <span data-ttu-id="91600-113">Necessaria Progetto a cui aggiungere reindirizzamenti di binding.</span><span class="sxs-lookup"><span data-stu-id="91600-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="91600-114">L'opzione-ProjectName è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="91600-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="91600-115">Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="91600-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="91600-116">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="91600-116">Common Parameters</span></span>

<span data-ttu-id="91600-117">`Add-BindingRedirect`supporta i seguenti [parametri comuni di PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="91600-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="91600-118">Esempi</span><span class="sxs-lookup"><span data-stu-id="91600-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```