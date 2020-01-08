---
title: Note sulla versione di NuGet 5,4
description: Note sulla versione per NuGet 5,4, incluse nuove funzionalità, correzioni di bug e DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: c7fb9c1e587b6603abe63581c662571abfd4506b
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384111"
---
# <a name="nuget-54-release-notes"></a><span data-ttu-id="0ce71-103">Note sulla versione di NuGet 5,4</span><span class="sxs-lookup"><span data-stu-id="0ce71-103">NuGet 5.4 Release Notes</span></span>

<span data-ttu-id="0ce71-104">Veicoli per la distribuzione di NuGet:</span><span class="sxs-lookup"><span data-stu-id="0ce71-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="0ce71-105">Versione di NuGet</span><span class="sxs-lookup"><span data-stu-id="0ce71-105">NuGet version</span></span> | <span data-ttu-id="0ce71-106">Disponibile nella versione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0ce71-106">Available in Visual Studio version</span></span>| <span data-ttu-id="0ce71-107">Disponibile in .NET SDK</span><span class="sxs-lookup"><span data-stu-id="0ce71-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="0ce71-108">**5.4.0**</span><span class="sxs-lookup"><span data-stu-id="0ce71-108">**5.4.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="0ce71-109">Visual Studio 2019 versione 16,4</span><span class="sxs-lookup"><span data-stu-id="0ce71-109">Visual Studio 2019 version 16.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="0ce71-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="0ce71-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="0ce71-111"><sup>1</sup> Installato con Visual Studio 2019 con carico di lavoro di .NET Core</span><span class="sxs-lookup"><span data-stu-id="0ce71-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-54"></a><span data-ttu-id="0ce71-112">Riepilogo: novità di 5,4</span><span class="sxs-lookup"><span data-stu-id="0ce71-112">Summary: What's New in 5.4</span></span>

* <span data-ttu-id="0ce71-113">Tempo di caricamento della soluzione più veloce: il sovraccarico del codice NuGet durante il primo caricamento della soluzione è stato ridotto tramite un NGen parziale per ridurre i costi JIT [#6007](https://github.com/NuGet/Home/issues/6007)</span><span class="sxs-lookup"><span data-stu-id="0ce71-113">Faster solution load time - Overhead running NuGet code during first solution load has been reduced via partial-ngen to reduce JIT cost - [#6007](https://github.com/NuGet/Home/issues/6007)</span></span>

* <span data-ttu-id="0ce71-114">Nuova funzione helper: dato un elenco di ID e versioni del pacchetto, ottenere i pacchetti di livello superiore probabili.</span><span class="sxs-lookup"><span data-stu-id="0ce71-114">New helper function - given a list of package ids and versions, get the likely top level packages.</span></span><span data-ttu-id="0ce71-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span><span class="sxs-lookup"><span data-stu-id="0ce71-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span></span>

* <span data-ttu-id="0ce71-116">Nuova azione [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) per l'installazione e la configurazione di NuGet. exe nelle [azioni di GitHub](https://github.com/features/actions).</span><span class="sxs-lookup"><span data-stu-id="0ce71-116">New [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) action for installing and configuring NuGet.exe on [GitHub Actions](https://github.com/features/actions).</span></span><span data-ttu-id="0ce71-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span><span class="sxs-lookup"><span data-stu-id="0ce71-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="0ce71-118">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="0ce71-118">Issues fixed in this release</span></span>

<span data-ttu-id="0ce71-119">**Bug**</span><span class="sxs-lookup"><span data-stu-id="0ce71-119">**Bugs**</span></span>

* <span data-ttu-id="0ce71-120">Plug-in: la precisione dell'ora di registrazione è disattivata in Linux/Mac- [#8747](https://github.com/NuGet/Home/issues/8747)</span><span class="sxs-lookup"><span data-stu-id="0ce71-120">Plugin: Logging time accuracy is off on linux/Mac - [#8747](https://github.com/NuGet/Home/issues/8747)</span></span>

* <span data-ttu-id="0ce71-121">L'eliminazione di un plug-in può talvolta generare e interrompere l'intera operazione.</span><span class="sxs-lookup"><span data-stu-id="0ce71-121">Disposing of a plugin can sometimes throw and fail the whole operation.</span></span><span data-ttu-id="0ce71-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span><span class="sxs-lookup"><span data-stu-id="0ce71-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span></span>

* <span data-ttu-id="0ce71-123">Interrompi la visualizzazione dei duplicati della versione nell'elenco delle versioni consentite e bloccate in PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)</span><span class="sxs-lookup"><span data-stu-id="0ce71-123">Stop displaying version duplicates in allowed and blocked versions list in PMUI - [#8679](https://github.com/NuGet/Home/issues/8679)</span></span>

* <span data-ttu-id="0ce71-124">Il file di blocco non è stato generato correttamente. l'ordinamento del Framework non dovrebbe avere alcun effetto sul ripristino con lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645)</span><span class="sxs-lookup"><span data-stu-id="0ce71-124">Lock File not properly generated - framework ordering should not impact the restore with lockedmode - [#8645](https://github.com/NuGet/Home/issues/8645)</span></span>

* <span data-ttu-id="0ce71-125">La convalida LockFile non riesce per i progetti con <RuntimeIdentifiers> impostati nell'SDK 3.0.100- [#8639](https://github.com/NuGet/Home/issues/8639)</span><span class="sxs-lookup"><span data-stu-id="0ce71-125">LockFile validation fails for projects with <RuntimeIdentifiers> set in SDK 3.0.100 - [#8639](https://github.com/NuGet/Home/issues/8639)</span></span>

* <span data-ttu-id="0ce71-126">La convalida della firma ora rifiuterà correttamente le firme con timestamp con due valori nello stesso OID- [#8629](https://github.com/NuGet/Home/issues/8629)</span><span class="sxs-lookup"><span data-stu-id="0ce71-126">Signing Validation will now properly reject signatures with timestamps which have 2 values under the same OID - [#8629](https://github.com/NuGet/Home/issues/8629)</span></span>

* <span data-ttu-id="0ce71-127">Aggiornare l'elenco di licenze- [#8544](https://github.com/NuGet/Home/issues/8544)</span><span class="sxs-lookup"><span data-stu-id="0ce71-127">Update the license list - [#8544](https://github.com/NuGet/Home/issues/8544)</span></span>

<span data-ttu-id="0ce71-128">**DCR**</span><span class="sxs-lookup"><span data-stu-id="0ce71-128">**DCRs**</span></span>

* <span data-ttu-id="0ce71-129">Onboarding dei file di diagnostica in IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535)</span><span class="sxs-lookup"><span data-stu-id="0ce71-129">Onboarding diagnostic files to IFeedbackDiagnosticFileProvider - [#8535](https://github.com/NuGet/Home/issues/8535)</span></span>

<span data-ttu-id="0ce71-130">**[Elenco di tutti i problemi risolti in questa versione-5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span><span class="sxs-lookup"><span data-stu-id="0ce71-130">**[List of all issues fixed in this release - 5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span></span>
