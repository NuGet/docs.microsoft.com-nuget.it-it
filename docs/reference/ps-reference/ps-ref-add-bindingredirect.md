---
title: Guida di riferimento a NuGet Add-BindingRedirect PowerShell
description: Informazioni di riferimento per il comando Add-BindingRedirect PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 382ba9b179428c70e3eb16db86a363e095207d61
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237257"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="f9e7d-103">Add-BindingRedirect (console di gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f9e7d-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f9e7d-104">*Disponibile solo nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="f9e7d-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="f9e7d-105">Esamina tutti gli assembly nel percorso di output di un progetto e aggiunge i reindirizzamenti di associazione al file di configurazione dell'applicazione o del Web, ove necessario.</span><span class="sxs-lookup"><span data-stu-id="f9e7d-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="f9e7d-106">Questo comando viene eseguito automaticamente durante l'installazione di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f9e7d-106">This command is run automatically when installing a package.</span></span>

> [!NOTE]
> <span data-ttu-id="f9e7d-107">Questo vale solo per gli scenari che usano un file di packages.config.</span><span class="sxs-lookup"><span data-stu-id="f9e7d-107">This only applies to scenarios using a packages.config file.</span></span> <span data-ttu-id="f9e7d-108">Per altre informazioni, vedere Guida di [riferimento ai file di packages.config NuGet](~/reference/packages-config.md).</span><span class="sxs-lookup"><span data-stu-id="f9e7d-108">For more information, see [NuGet packages.config file reference](~/reference/packages-config.md).</span></span>

<span data-ttu-id="f9e7d-109">Per informazioni dettagliate sui reindirizzamenti di binding e sul motivo per cui vengono usati, vedere [Reindirizzamento delle versioni degli assembly](/dotnet/framework/configure-apps/redirect-assembly-versions) nella documentazione di .NET.</span><span class="sxs-lookup"><span data-stu-id="f9e7d-109">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="f9e7d-110">Sintassi</span><span class="sxs-lookup"><span data-stu-id="f9e7d-110">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f9e7d-111">Parametri</span><span class="sxs-lookup"><span data-stu-id="f9e7d-111">Parameters</span></span>

| <span data-ttu-id="f9e7d-112">Parametro</span><span class="sxs-lookup"><span data-stu-id="f9e7d-112">Parameter</span></span> | <span data-ttu-id="f9e7d-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f9e7d-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f9e7d-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="f9e7d-114">ProjectName</span></span> | <span data-ttu-id="f9e7d-115">Necessaria Progetto a cui aggiungere reindirizzamenti di binding.</span><span class="sxs-lookup"><span data-stu-id="f9e7d-115">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="f9e7d-116">L'opzione-ProjectName è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="f9e7d-116">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="f9e7d-117">Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="f9e7d-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f9e7d-118">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="f9e7d-118">Common Parameters</span></span>

<span data-ttu-id="f9e7d-119">`Add-BindingRedirect` supporta i seguenti [parametri comuni di PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f9e7d-119">`Add-BindingRedirect` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f9e7d-120">Esempi</span><span class="sxs-lookup"><span data-stu-id="f9e7d-120">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```