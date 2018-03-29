---
title: NuGet CLI verificare comando | Documenti Microsoft
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Riferimento per il nuget.exe verificare comando
keywords: Verificare il riferimento, verificare di comando di NuGet
ms.reviewer:
- karann
- rmpablos
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4423e491e0ab5dc1e13982440db42bc9b0e85c38
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="91b48-104">Verificare di comando (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="91b48-104">verify command (NuGet CLI)</span></span>

<span data-ttu-id="91b48-105">**Si applica a:** pacchetto consumo &bullet; **le versioni supportate:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="91b48-105">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="91b48-106">Verifica di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="91b48-106">Verifies a package.</span></span>

## <a name="usage"></a><span data-ttu-id="91b48-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="91b48-107">Usage</span></span>

```cli
nuget verify <package(s)> [options]
```

<span data-ttu-id="91b48-108">dove `<package(s)>` uno o più `.nupkg` file.</span><span class="sxs-lookup"><span data-stu-id="91b48-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="91b48-109">Opzioni</span><span class="sxs-lookup"><span data-stu-id="91b48-109">Options</span></span>

| <span data-ttu-id="91b48-110">Opzione</span><span class="sxs-lookup"><span data-stu-id="91b48-110">Option</span></span> | <span data-ttu-id="91b48-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="91b48-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="91b48-112">Tutti</span><span class="sxs-lookup"><span data-stu-id="91b48-112">All</span></span> | <span data-ttu-id="91b48-113">Specifica che tutte le verifiche possibili devono essere eseguite in per i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="91b48-113">Specifies that all verifications possible should be performed on the package(s).</span></span> |
| <span data-ttu-id="91b48-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="91b48-114">CertificateFingerprint</span></span> | <span data-ttu-id="91b48-115">Specifica uno o più SHA-256 certificato le impronte digitali di certificati (s), i pacchetti firmati devono essere firmati con.</span><span class="sxs-lookup"><span data-stu-id="91b48-115">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="91b48-116">Un'impronta digitale certificato SHA-256 è un hash SHA-256 del certificato.</span><span class="sxs-lookup"><span data-stu-id="91b48-116">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="91b48-117">Più input devono essere separati da virgola.</span><span class="sxs-lookup"><span data-stu-id="91b48-117">Multiple inputs should be semicolon separated.</span></span> |
| <span data-ttu-id="91b48-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="91b48-118">ConfigFile</span></span> | <span data-ttu-id="91b48-119">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="91b48-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="91b48-120">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="91b48-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="91b48-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="91b48-121">ForceEnglishOutput</span></span> | <span data-ttu-id="91b48-122">Nuget.exe forza l'esecuzione utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="91b48-122">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="91b48-123">?</span><span class="sxs-lookup"><span data-stu-id="91b48-123">Help</span></span> | <span data-ttu-id="91b48-124">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="91b48-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="91b48-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="91b48-125">NonInteractive</span></span> | <span data-ttu-id="91b48-126">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="91b48-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="91b48-127">Firme</span><span class="sxs-lookup"><span data-stu-id="91b48-127">Signatures</span></span> | <span data-ttu-id="91b48-128">Specifica che deve essere eseguita la verifica della firma del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="91b48-128">Specifies that package signature verification should be performed.</span></span> |
| <span data-ttu-id="91b48-129">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="91b48-129">Verbosity</span></span> | <span data-ttu-id="91b48-130">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="91b48-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="91b48-131">Esempi</span><span class="sxs-lookup"><span data-stu-id="91b48-131">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```