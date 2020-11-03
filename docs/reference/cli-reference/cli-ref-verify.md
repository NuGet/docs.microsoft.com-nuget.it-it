---
title: Comando di verifica CLI di NuGet
description: Riferimento per il comando nuget.exe Verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7ce08f11195437e94bfe69883ff525e9ad3a73f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238140"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="aa84b-103">comando Verify (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="aa84b-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="aa84b-104">**Si applica a:** versioni supportate per l'utilizzo di pacchetti &bullet; **:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="aa84b-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="aa84b-105">Verifica un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="aa84b-105">Verifies a package.</span></span>

<span data-ttu-id="aa84b-106">La verifica dei pacchetti firmati non è ancora supportata in mono.</span><span class="sxs-lookup"><span data-stu-id="aa84b-106">Verification of signed packages is not yet supported under Mono.</span></span>

## <a name="usage"></a><span data-ttu-id="aa84b-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="aa84b-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="aa84b-108">dove `<package(s)>` è uno o più `.nupkg` file.</span><span class="sxs-lookup"><span data-stu-id="aa84b-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="aa84b-109">Verifica NuGet-tutto</span><span class="sxs-lookup"><span data-stu-id="aa84b-109">nuget verify -All</span></span>

<span data-ttu-id="aa84b-110">Specifica che tutte le verifiche possibili devono essere eseguite sui pacchetti.</span><span class="sxs-lookup"><span data-stu-id="aa84b-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="aa84b-111">Verifica NuGet-firme</span><span class="sxs-lookup"><span data-stu-id="aa84b-111">nuget verify -Signatures</span></span>

<span data-ttu-id="aa84b-112">Specifica che deve essere eseguita la verifica della firma del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="aa84b-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="aa84b-113">Opzioni per "Verifica-firme"</span><span class="sxs-lookup"><span data-stu-id="aa84b-113">Options for "verify -Signatures"</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="aa84b-114">Specifica una o più impronte digitali del certificato SHA-256 dei certificati i cui pacchetti firmati devono essere firmati.</span><span class="sxs-lookup"><span data-stu-id="aa84b-114">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="aa84b-115">Un'impronta digitale SHA-256 del certificato è un hash SHA-256 del certificato.</span><span class="sxs-lookup"><span data-stu-id="aa84b-115">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="aa84b-116">Più input devono essere separati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="aa84b-116">Multiple inputs should be semicolon separated.</span></span>

## <a name="options"></a><span data-ttu-id="aa84b-117">Opzioni</span><span class="sxs-lookup"><span data-stu-id="aa84b-117">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="aa84b-118">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="aa84b-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="aa84b-119">Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="aa84b-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="aa84b-120">Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="aa84b-120">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="aa84b-121">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="aa84b-121">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="aa84b-122">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="aa84b-122">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="aa84b-123">Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="aa84b-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="aa84b-124">Esempi</span><span class="sxs-lookup"><span data-stu-id="aa84b-124">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```