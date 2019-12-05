---
title: Note sulla versione di NuGet 5,4
description: Note sulla versione per NuGet 5,4, incluse nuove funzionalità, correzioni di bug e DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 69f78ba5483fcc92887624584663e8c496cfc497
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/04/2019
ms.locfileid: "74828408"
---
# <a name="nuget-54-release-notes"></a><span data-ttu-id="27c7d-103">Note sulla versione di NuGet 5,4</span><span class="sxs-lookup"><span data-stu-id="27c7d-103">NuGet 5.4 Release Notes</span></span>

<span data-ttu-id="27c7d-104">Veicoli per la distribuzione di NuGet:</span><span class="sxs-lookup"><span data-stu-id="27c7d-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="27c7d-105">Versione di NuGet</span><span class="sxs-lookup"><span data-stu-id="27c7d-105">NuGet version</span></span> | <span data-ttu-id="27c7d-106">Disponibile nella versione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="27c7d-106">Available in Visual Studio version</span></span>| <span data-ttu-id="27c7d-107">Disponibile in .NET SDK</span><span class="sxs-lookup"><span data-stu-id="27c7d-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="27c7d-108">**5.4.0**</span><span class="sxs-lookup"><span data-stu-id="27c7d-108">**5.4.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="27c7d-109">Visual Studio 2019 versione 16,4</span><span class="sxs-lookup"><span data-stu-id="27c7d-109">Visual Studio 2019 version 16.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="27c7d-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="27c7d-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="27c7d-111"><sup>1</sup> Installato con Visual Studio 2019 con carico di lavoro di .NET Core</span><span class="sxs-lookup"><span data-stu-id="27c7d-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-54"></a><span data-ttu-id="27c7d-112">Riepilogo: novità di 5,4</span><span class="sxs-lookup"><span data-stu-id="27c7d-112">Summary: What's New in 5.4</span></span>

* <span data-ttu-id="27c7d-113">Tempo di caricamento della soluzione più veloce: il sovraccarico del codice NuGet durante il primo caricamento della soluzione è stato ridotto tramite un NGen parziale per ridurre i costi JIT [#6007](https://github.com/NuGet/Home/issues/6007)</span><span class="sxs-lookup"><span data-stu-id="27c7d-113">Faster solution load time - Overhead running NuGet code during first solution load has been reduced via partial-ngen to reduce JIT cost - [#6007](https://github.com/NuGet/Home/issues/6007)</span></span>

* <span data-ttu-id="27c7d-114">Nuova funzione helper: dato un elenco di ID e versioni del pacchetto, ottenere i pacchetti di livello superiore probabili.</span><span class="sxs-lookup"><span data-stu-id="27c7d-114">New helper function - given a list of package ids and versions, get the likely top level packages.</span></span><span data-ttu-id="27c7d-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span><span class="sxs-lookup"><span data-stu-id="27c7d-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="27c7d-116">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="27c7d-116">Issues fixed in this release</span></span>

<span data-ttu-id="27c7d-117">**Bug**</span><span class="sxs-lookup"><span data-stu-id="27c7d-117">**Bugs**</span></span>

* <span data-ttu-id="27c7d-118">Plug-in: la precisione dell'ora di registrazione è disattivata in Linux/Mac- [#8747](https://github.com/NuGet/Home/issues/8747)</span><span class="sxs-lookup"><span data-stu-id="27c7d-118">Plugin: Logging time accuracy is off on linux/Mac - [#8747](https://github.com/NuGet/Home/issues/8747)</span></span>

* <span data-ttu-id="27c7d-119">L'eliminazione di un plug-in può talvolta generare e interrompere l'intera operazione.</span><span class="sxs-lookup"><span data-stu-id="27c7d-119">Disposing of a plugin can sometimes throw and fail the whole operation.</span></span><span data-ttu-id="27c7d-120"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span><span class="sxs-lookup"><span data-stu-id="27c7d-120"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span></span>

* <span data-ttu-id="27c7d-121">Interrompi la visualizzazione dei duplicati della versione nell'elenco delle versioni consentite e bloccate in PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)</span><span class="sxs-lookup"><span data-stu-id="27c7d-121">Stop displaying version duplicates in allowed and blocked versions list in PMUI - [#8679](https://github.com/NuGet/Home/issues/8679)</span></span>

* <span data-ttu-id="27c7d-122">Il file di blocco non è stato generato correttamente. l'ordinamento del Framework non dovrebbe avere alcun effetto sul ripristino con lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645)</span><span class="sxs-lookup"><span data-stu-id="27c7d-122">Lock File not properly generated - framework ordering should not impact the restore with lockedmode - [#8645](https://github.com/NuGet/Home/issues/8645)</span></span>

* <span data-ttu-id="27c7d-123">La convalida LockFile non riesce per i progetti con <RuntimeIdentifiers> impostati nell'SDK 3.0.100- [#8639](https://github.com/NuGet/Home/issues/8639)</span><span class="sxs-lookup"><span data-stu-id="27c7d-123">LockFile validation fails for projects with <RuntimeIdentifiers> set in SDK 3.0.100 - [#8639](https://github.com/NuGet/Home/issues/8639)</span></span>

* <span data-ttu-id="27c7d-124">La convalida della firma ora rifiuterà correttamente le firme con timestamp con due valori nello stesso OID- [#8629](https://github.com/NuGet/Home/issues/8629)</span><span class="sxs-lookup"><span data-stu-id="27c7d-124">Signing Validation will now properly reject signatures with timestamps which have 2 values under the same OID - [#8629](https://github.com/NuGet/Home/issues/8629)</span></span>

* <span data-ttu-id="27c7d-125">Aggiornare l'elenco di licenze- [#8544](https://github.com/NuGet/Home/issues/8544)</span><span class="sxs-lookup"><span data-stu-id="27c7d-125">Update the license list - [#8544](https://github.com/NuGet/Home/issues/8544)</span></span>

<span data-ttu-id="27c7d-126">**DCR**</span><span class="sxs-lookup"><span data-stu-id="27c7d-126">**DCRs**</span></span>

* <span data-ttu-id="27c7d-127">Onboarding dei file di diagnostica in IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535)</span><span class="sxs-lookup"><span data-stu-id="27c7d-127">Onboarding diagnostic files to IFeedbackDiagnosticFileProvider - [#8535](https://github.com/NuGet/Home/issues/8535)</span></span>

<span data-ttu-id="27c7d-128">**[Elenco di tutti i problemi risolti in questa versione-5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span><span class="sxs-lookup"><span data-stu-id="27c7d-128">**[List of all issues fixed in this release - 5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span></span>
