---
title: Comando di verifica CLI di NuGet
description: Informazioni di riferimento sul comando NuGet. exe verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327498"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="f670b-103">Comando verify (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="f670b-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="f670b-104">**Si applica a:** &bullet; **versioni supportate** per l'utilizzo di pacchetti: 4.6 +</span><span class="sxs-lookup"><span data-stu-id="f670b-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="f670b-105">Verifica un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f670b-105">Verifies a package.</span></span>

<span data-ttu-id="f670b-106">La verifica dei pacchetti firmati non è ancora supportata in .NET Core, in mono o in piattaforme non Windows.</span><span class="sxs-lookup"><span data-stu-id="f670b-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="f670b-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="f670b-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="f670b-108">dove `<package(s)>` è uno o più `.nupkg` file.</span><span class="sxs-lookup"><span data-stu-id="f670b-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="f670b-109">Verifica NuGet-tutto</span><span class="sxs-lookup"><span data-stu-id="f670b-109">nuget verify -All</span></span>

<span data-ttu-id="f670b-110">Specifica che tutte le verifiche possibili devono essere eseguite sui pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f670b-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="f670b-111">Verifica NuGet-firme</span><span class="sxs-lookup"><span data-stu-id="f670b-111">nuget verify -Signatures</span></span>

<span data-ttu-id="f670b-112">Specifica che deve essere eseguita la verifica della firma del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f670b-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="f670b-113">Opzioni per "Verifica-firme"</span><span class="sxs-lookup"><span data-stu-id="f670b-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="f670b-114">Opzione</span><span class="sxs-lookup"><span data-stu-id="f670b-114">Option</span></span> | <span data-ttu-id="f670b-115">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f670b-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f670b-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="f670b-116">CertificateFingerprint</span></span> | <span data-ttu-id="f670b-117">Specifica una o più impronte digitali del certificato SHA-256 dei certificati i cui pacchetti firmati devono essere firmati.</span><span class="sxs-lookup"><span data-stu-id="f670b-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="f670b-118">Un'impronta digitale SHA-256 del certificato è un hash SHA-256 del certificato.</span><span class="sxs-lookup"><span data-stu-id="f670b-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="f670b-119">Più input devono essere separati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="f670b-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="f670b-120">Opzioni</span><span class="sxs-lookup"><span data-stu-id="f670b-120">Options</span></span>

| <span data-ttu-id="f670b-121">Opzione</span><span class="sxs-lookup"><span data-stu-id="f670b-121">Option</span></span> | <span data-ttu-id="f670b-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f670b-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f670b-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f670b-123">ConfigFile</span></span> | <span data-ttu-id="f670b-124">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="f670b-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f670b-125">Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="f670b-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f670b-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f670b-126">ForceEnglishOutput</span></span> | <span data-ttu-id="f670b-127">Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese.</span><span class="sxs-lookup"><span data-stu-id="f670b-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f670b-128">?</span><span class="sxs-lookup"><span data-stu-id="f670b-128">Help</span></span> | <span data-ttu-id="f670b-129">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="f670b-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="f670b-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="f670b-130">Verbosity</span></span> | <span data-ttu-id="f670b-131">Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*.</span><span class="sxs-lookup"><span data-stu-id="f670b-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="f670b-132">Esempi</span><span class="sxs-lookup"><span data-stu-id="f670b-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```