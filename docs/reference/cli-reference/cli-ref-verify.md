---
title: Comando di verifica CLI di NuGet
description: Riferimento per il comando nuget.exe Verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 2c501753a16820c5d027441001561c6b637ccda9
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622603"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="a5dc4-103">comando Verify (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="a5dc4-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="a5dc4-104">**Si applica a:** versioni supportate per l'utilizzo di pacchetti &bullet; **:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="a5dc4-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="a5dc4-105">Verifica un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a5dc4-105">Verifies a package.</span></span>

<span data-ttu-id="a5dc4-106">La verifica dei pacchetti firmati non è ancora supportata in .NET Core, in mono o in piattaforme non Windows.</span><span class="sxs-lookup"><span data-stu-id="a5dc4-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="a5dc4-107">Uso</span><span class="sxs-lookup"><span data-stu-id="a5dc4-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="a5dc4-108">dove `<package(s)>` è uno o più `.nupkg` file.</span><span class="sxs-lookup"><span data-stu-id="a5dc4-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="a5dc4-109">Verifica NuGet-tutto</span><span class="sxs-lookup"><span data-stu-id="a5dc4-109">nuget verify -All</span></span>

<span data-ttu-id="a5dc4-110">Specifica che tutte le verifiche possibili devono essere eseguite sui pacchetti.</span><span class="sxs-lookup"><span data-stu-id="a5dc4-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="a5dc4-111">Verifica NuGet-firme</span><span class="sxs-lookup"><span data-stu-id="a5dc4-111">nuget verify -Signatures</span></span>

<span data-ttu-id="a5dc4-112">Specifica che deve essere eseguita la verifica della firma del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a5dc4-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="a5dc4-113">Opzioni per "Verifica-firme"</span><span class="sxs-lookup"><span data-stu-id="a5dc4-113">Options for "verify -Signatures"</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="a5dc4-114">Specifica una o più impronte digitali del certificato SHA-256 dei certificati i cui pacchetti firmati devono essere firmati.</span><span class="sxs-lookup"><span data-stu-id="a5dc4-114">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="a5dc4-115">Un'impronta digitale SHA-256 del certificato è un hash SHA-256 del certificato.</span><span class="sxs-lookup"><span data-stu-id="a5dc4-115">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="a5dc4-116">Più input devono essere separati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="a5dc4-116">Multiple inputs should be semicolon separated.</span></span>

## <a name="options"></a><span data-ttu-id="a5dc4-117">Opzioni</span><span class="sxs-lookup"><span data-stu-id="a5dc4-117">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="a5dc4-118">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="a5dc4-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a5dc4-119">Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="a5dc4-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="a5dc4-120">Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="a5dc4-120">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="a5dc4-121">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="a5dc4-121">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="a5dc4-122">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a5dc4-122">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="a5dc4-123">Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="a5dc4-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="a5dc4-124">Esempi</span><span class="sxs-lookup"><span data-stu-id="a5dc4-124">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```