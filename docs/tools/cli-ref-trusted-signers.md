---
title: Comando di NuGet CLI firmatari attendibili
description: Informazioni di riferimento per il comando di firmatari attendibili nuget.exe
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: ffd0cf5d50a2deed16e1722b32e43047bc81df2f
ms.sourcegitcommit: a1846edf70ddb2505d58e536e08e952d870931b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/26/2018
ms.locfileid: "52303687"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="6b385-103">comando firmatari attendibili (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="6b385-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="6b385-104">**Si applica a:** consumo del pacchetto &bullet; **le versioni supportate:** 4.9 +</span><span class="sxs-lookup"><span data-stu-id="6b385-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9+</span></span>

<span data-ttu-id="6b385-105">Ottiene o imposta i firmatari attendibili per la configurazione di NuGet.</span><span class="sxs-lookup"><span data-stu-id="6b385-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="6b385-106">Per altre informazioni sulla sintassi, vedere [configurazione del comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="6b385-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="6b385-107">Per informazioni dettagliate su come lo schema di NuGet. config sembra, vedere la [riferimento al file di configurazione NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="6b385-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="6b385-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="6b385-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="6b385-109">Se nessuna delle `list|add|remove|sync` viene specificato, il comando per impostazione predefinita sarà `list`.</span><span class="sxs-lookup"><span data-stu-id="6b385-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="6b385-110">elenco di firmatari attendibili di NuGet</span><span class="sxs-lookup"><span data-stu-id="6b385-110">nuget trusted-signers list</span></span>

<span data-ttu-id="6b385-111">Elenca tutti i firmatari attendibili nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="6b385-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="6b385-112">Questa opzione includerà tutti i certificati, con impronta digitale e algoritmo di impronta digitale, con ogni firmatario.</span><span class="sxs-lookup"><span data-stu-id="6b385-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="6b385-113">Se un certificato con una precedente `[U]`, significa che la voce certificato ha `allowUntrustedRoot` imposta come `true`.</span><span class="sxs-lookup"><span data-stu-id="6b385-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="6b385-114">Di seguito è un esempio di output da questo comando:</span><span class="sxs-lookup"><span data-stu-id="6b385-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="6b385-115">attendibili i firmatari NuGet add [opzioni]</span><span class="sxs-lookup"><span data-stu-id="6b385-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="6b385-116">Aggiunge un'entità attendibile con il nome specificato al file di configurazione. Questa opzione non ha i movimenti diversi per aggiungere un repository o autore attendibile.</span><span class="sxs-lookup"><span data-stu-id="6b385-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="6b385-117">Opzioni per l'aggiunta in un pacchetto di base</span><span class="sxs-lookup"><span data-stu-id="6b385-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="6b385-118">in cui `<package(s)>` è uno o più `.nupkg` file.</span><span class="sxs-lookup"><span data-stu-id="6b385-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="6b385-119">Opzione</span><span class="sxs-lookup"><span data-stu-id="6b385-119">Option</span></span> | <span data-ttu-id="6b385-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6b385-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6b385-121">Autore</span><span class="sxs-lookup"><span data-stu-id="6b385-121">Author</span></span> | <span data-ttu-id="6b385-122">Specifica che la firma dell'autore dei pacchetti debba essere attendibile.</span><span class="sxs-lookup"><span data-stu-id="6b385-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="6b385-123">Repository</span><span class="sxs-lookup"><span data-stu-id="6b385-123">Repository</span></span> | <span data-ttu-id="6b385-124">Specifica che la firma di repository o controfirma dei pacchetti deve essere considerato attendibile.</span><span class="sxs-lookup"><span data-stu-id="6b385-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="6b385-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="6b385-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="6b385-126">Specifica se il certificato del firmatario attendibile deve essere consentito concatenarsi a una radice non attendibile.</span><span class="sxs-lookup"><span data-stu-id="6b385-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="6b385-127">Proprietari</span><span class="sxs-lookup"><span data-stu-id="6b385-127">Owners</span></span> | <span data-ttu-id="6b385-128">Elenco separato da punti e virgola dei proprietari attendibili per limitare ulteriormente l'attendibilità di un repository.</span><span class="sxs-lookup"><span data-stu-id="6b385-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="6b385-129">Valido solo quando si usa il `-Repository` opzione.</span><span class="sxs-lookup"><span data-stu-id="6b385-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="6b385-130">Forniscono `-Author` e `-Repository` allo stesso tempo non è supportato.</span><span class="sxs-lookup"><span data-stu-id="6b385-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="6b385-131">Opzioni Aggiungi basato su un indice di servizio</span><span class="sxs-lookup"><span data-stu-id="6b385-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="6b385-132">_Nota_: consente solo di aggiungere repository attendibile.</span><span class="sxs-lookup"><span data-stu-id="6b385-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="6b385-133">Opzione</span><span class="sxs-lookup"><span data-stu-id="6b385-133">Option</span></span> | <span data-ttu-id="6b385-134">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6b385-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6b385-135">ServiceIndex</span><span class="sxs-lookup"><span data-stu-id="6b385-135">ServiceIndex</span></span> | <span data-ttu-id="6b385-136">Specifica l'indice del servizio V3 del repository per essere considerato attendibile.</span><span class="sxs-lookup"><span data-stu-id="6b385-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="6b385-137">Questo repository deve supportare la risorsa di firme di repository.</span><span class="sxs-lookup"><span data-stu-id="6b385-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="6b385-138">Se non specificato, il comando cercherà il file di origine con lo stesso `-Name` e ottenere l'indice del servizio da tale posizione.</span><span class="sxs-lookup"><span data-stu-id="6b385-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="6b385-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="6b385-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="6b385-140">Specifica se il certificato del firmatario attendibile deve essere consentito concatenarsi a una radice non attendibile.</span><span class="sxs-lookup"><span data-stu-id="6b385-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="6b385-141">Proprietari</span><span class="sxs-lookup"><span data-stu-id="6b385-141">Owners</span></span> | <span data-ttu-id="6b385-142">Elenco separato da punti e virgola dei proprietari attendibili per limitare ulteriormente l'attendibilità di un repository.</span><span class="sxs-lookup"><span data-stu-id="6b385-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="6b385-143">Opzioni per aggiungere le informazioni sul certificato in base</span><span class="sxs-lookup"><span data-stu-id="6b385-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="6b385-144">_Nota_: se un'entità attendibile con il nome specificato esiste già, verrà aggiunto l'elemento certificato per tale firmatario.</span><span class="sxs-lookup"><span data-stu-id="6b385-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="6b385-145">In caso contrario, verrà creato un autore attendibile a un elemento di certificato da fornito informazioni sul certificato.</span><span class="sxs-lookup"><span data-stu-id="6b385-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="6b385-146">Opzione</span><span class="sxs-lookup"><span data-stu-id="6b385-146">Option</span></span> | <span data-ttu-id="6b385-147">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6b385-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6b385-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="6b385-148">CertificateFingerprint</span></span> | <span data-ttu-id="6b385-149">Specifica un certificato le impronte digitali di un certificato di pacchetti firmati devono essere firmate con.</span><span class="sxs-lookup"><span data-stu-id="6b385-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="6b385-150">Un'impronta digitale certificato è un hash del certificato.</span><span class="sxs-lookup"><span data-stu-id="6b385-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="6b385-151">Specifica l'algoritmo hash usato per calcolare l'hash deve essere il `FingerprintAlgorithm` opzione.</span><span class="sxs-lookup"><span data-stu-id="6b385-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="6b385-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="6b385-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="6b385-153">Specifica l'algoritmo hash usato per calcolare l'impronta digitale del certificato.</span><span class="sxs-lookup"><span data-stu-id="6b385-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="6b385-154">Il valore predefinito è `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="6b385-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="6b385-155">Valori supportati sono `SHA256`, `SHA384` e `SHA512`</span><span class="sxs-lookup"><span data-stu-id="6b385-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="6b385-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="6b385-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="6b385-157">Specifica se il certificato del firmatario attendibile deve essere consentito concatenarsi a una radice non attendibile.</span><span class="sxs-lookup"><span data-stu-id="6b385-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="6b385-158">rimuovere i firmatari attendibile-NuGet - nome <name></span><span class="sxs-lookup"><span data-stu-id="6b385-158">nuget trusted-signers remove -Name <name></span></span>

<span data-ttu-id="6b385-159">Rimuove tutti i firmatari attendibili che corrispondono al nome specificato.</span><span class="sxs-lookup"><span data-stu-id="6b385-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="6b385-160">sincronizzare i firmatari attendibile-NuGet - nome <name></span><span class="sxs-lookup"><span data-stu-id="6b385-160">nuget trusted-signers sync -Name <name></span></span>

<span data-ttu-id="6b385-161">Richiede l'elenco più recente di certificati usata in un repository attualmente considerato attendibile per aggiornare l'elenco certificato esistente in un'entità attendibile.</span><span class="sxs-lookup"><span data-stu-id="6b385-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="6b385-162">_Nota_: questa azione verrà Elimina l'elenco corrente dei certificati e li sostituisce con un elenco aggiornato dal repository.</span><span class="sxs-lookup"><span data-stu-id="6b385-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="6b385-163">Opzioni</span><span class="sxs-lookup"><span data-stu-id="6b385-163">Options</span></span>

| <span data-ttu-id="6b385-164">Opzione</span><span class="sxs-lookup"><span data-stu-id="6b385-164">Option</span></span> | <span data-ttu-id="6b385-165">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6b385-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6b385-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="6b385-166">ConfigFile</span></span> | <span data-ttu-id="6b385-167">Il file di configurazione di NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="6b385-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6b385-168">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.</span><span class="sxs-lookup"><span data-stu-id="6b385-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="6b385-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="6b385-169">ForceEnglishOutput</span></span> | <span data-ttu-id="6b385-170">Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="6b385-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="6b385-171">?</span><span class="sxs-lookup"><span data-stu-id="6b385-171">Help</span></span> | <span data-ttu-id="6b385-172">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="6b385-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="6b385-173">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="6b385-173">Verbosity</span></span> | <span data-ttu-id="6b385-174">Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="6b385-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="6b385-175">Esempi</span><span class="sxs-lookup"><span data-stu-id="6b385-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```