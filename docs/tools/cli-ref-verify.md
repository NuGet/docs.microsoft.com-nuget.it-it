---
title: NuGet CLI verificare comando
description: Riferimento per il nuget.exe verificare comando
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c80334104f7d8b2ccbf16ea2c11dc37b39408eeb
ms.sourcegitcommit: c8485dc61469511485367d2067b97d6f74b49f6e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="cc32c-103">Comando verify (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="cc32c-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="cc32c-104">**Si applica a:** pacchetto consumo &bullet; **le versioni supportate:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="cc32c-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="cc32c-105">Verifica di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cc32c-105">Verifies a package.</span></span>

<span data-ttu-id="cc32c-106">Verifica dei pacchetti con segno non è ancora supportata in .NET Core, in Mono o su piattaforme non Windows.</span><span class="sxs-lookup"><span data-stu-id="cc32c-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="cc32c-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="cc32c-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="cc32c-108">dove `<package(s)>` uno o più `.nupkg` file.</span><span class="sxs-lookup"><span data-stu-id="cc32c-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="cc32c-109">Verificare che NuGet - tutto</span><span class="sxs-lookup"><span data-stu-id="cc32c-109">nuget verify -All</span></span>

<span data-ttu-id="cc32c-110">Specifica che tutte le verifiche possibili devono essere eseguite in per i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cc32c-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="cc32c-111">Verificare di NuGet - firme</span><span class="sxs-lookup"><span data-stu-id="cc32c-111">nuget verify -Signatures</span></span>

<span data-ttu-id="cc32c-112">Specifica che deve essere eseguita la verifica della firma del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cc32c-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="cc32c-113">Opzioni per "verificare - firme"</span><span class="sxs-lookup"><span data-stu-id="cc32c-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="cc32c-114">Opzione</span><span class="sxs-lookup"><span data-stu-id="cc32c-114">Option</span></span> | <span data-ttu-id="cc32c-115">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cc32c-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc32c-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="cc32c-116">CertificateFingerprint</span></span> | <span data-ttu-id="cc32c-117">Specifica uno o più SHA-256 certificato le impronte digitali di certificati (s), i pacchetti firmati devono essere firmati con.</span><span class="sxs-lookup"><span data-stu-id="cc32c-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="cc32c-118">Un'impronta digitale certificato SHA-256 è un hash SHA-256 del certificato.</span><span class="sxs-lookup"><span data-stu-id="cc32c-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="cc32c-119">Più input devono essere separati da virgola.</span><span class="sxs-lookup"><span data-stu-id="cc32c-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="cc32c-120">Opzioni</span><span class="sxs-lookup"><span data-stu-id="cc32c-120">Options</span></span>

| <span data-ttu-id="cc32c-121">Opzione</span><span class="sxs-lookup"><span data-stu-id="cc32c-121">Option</span></span> | <span data-ttu-id="cc32c-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cc32c-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc32c-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="cc32c-123">ConfigFile</span></span> | <span data-ttu-id="cc32c-124">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="cc32c-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cc32c-125">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="cc32c-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="cc32c-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="cc32c-126">ForceEnglishOutput</span></span> | <span data-ttu-id="cc32c-127">Nuget.exe forza l'esecuzione utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="cc32c-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="cc32c-128">?</span><span class="sxs-lookup"><span data-stu-id="cc32c-128">Help</span></span> | <span data-ttu-id="cc32c-129">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="cc32c-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="cc32c-130">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="cc32c-130">Verbosity</span></span> | <span data-ttu-id="cc32c-131">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="cc32c-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="cc32c-132">Esempi</span><span class="sxs-lookup"><span data-stu-id="cc32c-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```