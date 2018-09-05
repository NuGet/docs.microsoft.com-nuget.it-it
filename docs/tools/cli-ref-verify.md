---
title: NuGet CLI verificare comando
description: Informazioni di riferimento per il nuget.exe verificare comando
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 127f7a549c0a213f319c8820293646b302830436
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545213"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="de76f-103">Comando verify (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="de76f-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="de76f-104">**Si applica a:** consumo del pacchetto &bullet; **le versioni supportate:** 4.6 e versioni successive</span><span class="sxs-lookup"><span data-stu-id="de76f-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="de76f-105">Verifica di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="de76f-105">Verifies a package.</span></span>

<span data-ttu-id="de76f-106">Verifica dei pacchetti firmati non è ancora supportata in .NET Core, in Mono, o su piattaforme non Windows.</span><span class="sxs-lookup"><span data-stu-id="de76f-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="de76f-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="de76f-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="de76f-108">in cui `<package(s)>` è uno o più `.nupkg` file.</span><span class="sxs-lookup"><span data-stu-id="de76f-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="de76f-109">NuGet verifica - tutto</span><span class="sxs-lookup"><span data-stu-id="de76f-109">nuget verify -All</span></span>

<span data-ttu-id="de76f-110">Specifica che tutte le verifiche possibili devono essere eseguite sui pacchetti.</span><span class="sxs-lookup"><span data-stu-id="de76f-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="de76f-111">NuGet verifica - firme</span><span class="sxs-lookup"><span data-stu-id="de76f-111">nuget verify -Signatures</span></span>

<span data-ttu-id="de76f-112">Specifica che deve essere eseguita la verifica della firma del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="de76f-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="de76f-113">Opzioni per "verificare - firme"</span><span class="sxs-lookup"><span data-stu-id="de76f-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="de76f-114">Opzione</span><span class="sxs-lookup"><span data-stu-id="de76f-114">Option</span></span> | <span data-ttu-id="de76f-115">Descrizione</span><span class="sxs-lookup"><span data-stu-id="de76f-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de76f-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="de76f-116">CertificateFingerprint</span></span> | <span data-ttu-id="de76f-117">Specifica uno o più SHA-256 certificato le impronte digitali dei quali pacchetti firmati devono essere firmati con certificati (s).</span><span class="sxs-lookup"><span data-stu-id="de76f-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="de76f-118">Un'impronta digitale certificato SHA-256 è un hash SHA-256 del certificato.</span><span class="sxs-lookup"><span data-stu-id="de76f-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="de76f-119">Più input deve essere delimitato da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="de76f-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="de76f-120">Opzioni</span><span class="sxs-lookup"><span data-stu-id="de76f-120">Options</span></span>

| <span data-ttu-id="de76f-121">Opzione</span><span class="sxs-lookup"><span data-stu-id="de76f-121">Option</span></span> | <span data-ttu-id="de76f-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="de76f-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de76f-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="de76f-123">ConfigFile</span></span> | <span data-ttu-id="de76f-124">Il file di configurazione di NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="de76f-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="de76f-125">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.</span><span class="sxs-lookup"><span data-stu-id="de76f-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="de76f-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="de76f-126">ForceEnglishOutput</span></span> | <span data-ttu-id="de76f-127">Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="de76f-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="de76f-128">?</span><span class="sxs-lookup"><span data-stu-id="de76f-128">Help</span></span> | <span data-ttu-id="de76f-129">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="de76f-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="de76f-130">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="de76f-130">Verbosity</span></span> | <span data-ttu-id="de76f-131">Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="de76f-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="de76f-132">Esempi</span><span class="sxs-lookup"><span data-stu-id="de76f-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```