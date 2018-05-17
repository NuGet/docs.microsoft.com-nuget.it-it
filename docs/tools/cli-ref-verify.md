---
title: NuGet CLI verificare comando
description: Riferimento per il nuget.exe verificare comando
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c2c31b71358bc50a1fb9aab8905c279cd1235b07
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="67c97-103">Comando verify (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="67c97-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="67c97-104">**Si applica a:** pacchetto consumo &bullet; **le versioni supportate:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="67c97-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="67c97-105">Verifica di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="67c97-105">Verifies a package.</span></span>

<span data-ttu-id="67c97-106">Verifica dei pacchetti con segno non è ancora supportata in .NET Core, in Mono o su piattaforme non Windows.</span><span class="sxs-lookup"><span data-stu-id="67c97-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="67c97-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="67c97-107">Usage</span></span>

```cli
nuget verify <package(s)> [options]
```

<span data-ttu-id="67c97-108">dove `<package(s)>` uno o più `.nupkg` file.</span><span class="sxs-lookup"><span data-stu-id="67c97-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="67c97-109">Opzioni</span><span class="sxs-lookup"><span data-stu-id="67c97-109">Options</span></span>

| <span data-ttu-id="67c97-110">Opzione</span><span class="sxs-lookup"><span data-stu-id="67c97-110">Option</span></span> | <span data-ttu-id="67c97-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="67c97-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="67c97-112">Tutti</span><span class="sxs-lookup"><span data-stu-id="67c97-112">All</span></span> | <span data-ttu-id="67c97-113">Specifica che tutte le verifiche possibili devono essere eseguite in per i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="67c97-113">Specifies that all verifications possible should be performed on the package(s).</span></span> |
| <span data-ttu-id="67c97-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="67c97-114">CertificateFingerprint</span></span> | <span data-ttu-id="67c97-115">Specifica uno o più SHA-256 certificato le impronte digitali di certificati (s), i pacchetti firmati devono essere firmati con.</span><span class="sxs-lookup"><span data-stu-id="67c97-115">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="67c97-116">Un'impronta digitale certificato SHA-256 è un hash SHA-256 del certificato.</span><span class="sxs-lookup"><span data-stu-id="67c97-116">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="67c97-117">Più input devono essere separati da virgola.</span><span class="sxs-lookup"><span data-stu-id="67c97-117">Multiple inputs should be semicolon separated.</span></span> |
| <span data-ttu-id="67c97-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="67c97-118">ConfigFile</span></span> | <span data-ttu-id="67c97-119">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="67c97-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="67c97-120">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="67c97-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="67c97-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="67c97-121">ForceEnglishOutput</span></span> | <span data-ttu-id="67c97-122">Nuget.exe forza l'esecuzione utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="67c97-122">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="67c97-123">?</span><span class="sxs-lookup"><span data-stu-id="67c97-123">Help</span></span> | <span data-ttu-id="67c97-124">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="67c97-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="67c97-125">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="67c97-125">NonInteractive</span></span> | <span data-ttu-id="67c97-126">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="67c97-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="67c97-127">Firme</span><span class="sxs-lookup"><span data-stu-id="67c97-127">Signatures</span></span> | <span data-ttu-id="67c97-128">Specifica che deve essere eseguita la verifica della firma del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="67c97-128">Specifies that package signature verification should be performed.</span></span> |
| <span data-ttu-id="67c97-129">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="67c97-129">Verbosity</span></span> | <span data-ttu-id="67c97-130">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="67c97-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="67c97-131">Esempi</span><span class="sxs-lookup"><span data-stu-id="67c97-131">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```