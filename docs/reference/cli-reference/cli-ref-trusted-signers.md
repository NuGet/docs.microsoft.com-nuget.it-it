---
title: Comando per i firmatari dell'interfaccia della riga di comando di NuGet
description: Informazioni di riferimento per il comando del firmatario attendibile NuGet. exe
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 94c4c6524c1870898893b80be914477af5a14e8b
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610339"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="6735c-103">comando Trusted-signers (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="6735c-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="6735c-104">**Si applica a:** uso del pacchetto &bullet; **versioni supportate:** 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="6735c-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="6735c-105">Ottiene o imposta i firmatari attendibili per la configurazione NuGet.</span><span class="sxs-lookup"><span data-stu-id="6735c-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="6735c-106">Per ulteriori informazioni sull'utilizzo, vedere [configurazioni comuni di NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="6735c-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="6735c-107">Per informazioni dettagliate sull'aspetto dello schema NuGet. config, vedere il riferimento al [file di configurazione NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="6735c-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="6735c-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="6735c-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="6735c-109">Se non viene specificato alcun `list|add|remove|sync`, per impostazione predefinita il comando verrà `list`.</span><span class="sxs-lookup"><span data-stu-id="6735c-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="6735c-110">elenco di firmatari attendibili NuGet</span><span class="sxs-lookup"><span data-stu-id="6735c-110">nuget trusted-signers list</span></span>

<span data-ttu-id="6735c-111">Elenca tutti i firmatari attendibili nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="6735c-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="6735c-112">Questa opzione includerà tutti i certificati (con algoritmo di impronta digitale e impronta digitale) di ogni firmatario.</span><span class="sxs-lookup"><span data-stu-id="6735c-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="6735c-113">Se un certificato ha un `[U]`precedente, significa che la voce del certificato ha `allowUntrustedRoot` impostato come `true`.</span><span class="sxs-lookup"><span data-stu-id="6735c-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="6735c-114">Di seguito è riportato un esempio di output di questo comando:</span><span class="sxs-lookup"><span data-stu-id="6735c-114">Below is an example output from this command:</span></span>

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

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="6735c-115">NuGet Trusted-signers Add [opzioni]</span><span class="sxs-lookup"><span data-stu-id="6735c-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="6735c-116">Aggiunge al file di configurazione un firmatario attendibile con il nome specificato. Questa opzione ha movimenti diversi per aggiungere un autore o un repository attendibile.</span><span class="sxs-lookup"><span data-stu-id="6735c-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="6735c-117">Opzioni per l'aggiunta in base a un pacchetto</span><span class="sxs-lookup"><span data-stu-id="6735c-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="6735c-118">dove `<package(s)>` è uno o più file di `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="6735c-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="6735c-119">Opzione</span><span class="sxs-lookup"><span data-stu-id="6735c-119">Option</span></span> | <span data-ttu-id="6735c-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6735c-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6735c-121">Autore</span><span class="sxs-lookup"><span data-stu-id="6735c-121">Author</span></span> | <span data-ttu-id="6735c-122">Specifica che la firma dell'autore dei pacchetti deve essere attendibile.</span><span class="sxs-lookup"><span data-stu-id="6735c-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="6735c-123">Repository</span><span class="sxs-lookup"><span data-stu-id="6735c-123">Repository</span></span> | <span data-ttu-id="6735c-124">Specifica che la firma del repository o il controfirma dei pacchetti deve essere attendibile.</span><span class="sxs-lookup"><span data-stu-id="6735c-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="6735c-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="6735c-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="6735c-126">Specifica se il certificato per il firmatario attendibile deve essere concatenato a una radice non attendibile.</span><span class="sxs-lookup"><span data-stu-id="6735c-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="6735c-127">Proprietari</span><span class="sxs-lookup"><span data-stu-id="6735c-127">Owners</span></span> | <span data-ttu-id="6735c-128">Elenco separato da punto e virgola di proprietari attendibili per limitare ulteriormente la relazione di trust di un repository.</span><span class="sxs-lookup"><span data-stu-id="6735c-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="6735c-129">Valido solo quando si usa l'opzione `-Repository`.</span><span class="sxs-lookup"><span data-stu-id="6735c-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="6735c-130">Non è supportata la fornitura di `-Author` e `-Repository` contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="6735c-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="6735c-131">Opzioni per l'aggiunta in base a un indice del servizio</span><span class="sxs-lookup"><span data-stu-id="6735c-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="6735c-132">_Nota_: questa opzione consente di aggiungere solo repository attendibili.</span><span class="sxs-lookup"><span data-stu-id="6735c-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="6735c-133">Opzione</span><span class="sxs-lookup"><span data-stu-id="6735c-133">Option</span></span> | <span data-ttu-id="6735c-134">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6735c-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6735c-135">ServiceIndex</span><span class="sxs-lookup"><span data-stu-id="6735c-135">ServiceIndex</span></span> | <span data-ttu-id="6735c-136">Specifica l'indice del servizio V3 del repository da ritenere attendibile.</span><span class="sxs-lookup"><span data-stu-id="6735c-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="6735c-137">Questo repository deve supportare la risorsa delle firme del repository.</span><span class="sxs-lookup"><span data-stu-id="6735c-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="6735c-138">Se non viene specificato, il comando cercherà un'origine del pacchetto con lo stesso `-Name` e otterrà l'indice del servizio.</span><span class="sxs-lookup"><span data-stu-id="6735c-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="6735c-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="6735c-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="6735c-140">Specifica se il certificato per il firmatario attendibile deve essere concatenato a una radice non attendibile.</span><span class="sxs-lookup"><span data-stu-id="6735c-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="6735c-141">Proprietari</span><span class="sxs-lookup"><span data-stu-id="6735c-141">Owners</span></span> | <span data-ttu-id="6735c-142">Elenco separato da punto e virgola di proprietari attendibili per limitare ulteriormente la relazione di trust di un repository.</span><span class="sxs-lookup"><span data-stu-id="6735c-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="6735c-143">Opzioni per l'aggiunta in base alle informazioni sul certificato</span><span class="sxs-lookup"><span data-stu-id="6735c-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="6735c-144">_Nota_: se un firmatario attendibile con il nome specificato esiste già, l'elemento del certificato verrà aggiunto a tale firmatario.</span><span class="sxs-lookup"><span data-stu-id="6735c-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="6735c-145">In caso contrario, verrà creato un autore attendibile con un elemento certificato fornito dalle informazioni del certificato.</span><span class="sxs-lookup"><span data-stu-id="6735c-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="6735c-146">Opzione</span><span class="sxs-lookup"><span data-stu-id="6735c-146">Option</span></span> | <span data-ttu-id="6735c-147">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6735c-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6735c-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="6735c-148">CertificateFingerprint</span></span> | <span data-ttu-id="6735c-149">Specifica le impronte digitali di un certificato con cui devono essere firmati i pacchetti firmati.</span><span class="sxs-lookup"><span data-stu-id="6735c-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="6735c-150">Un'impronta digitale del certificato è un hash del certificato.</span><span class="sxs-lookup"><span data-stu-id="6735c-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="6735c-151">L'algoritmo hash usato per il calcolo di questo hash deve essere specificato nell'opzione `FingerprintAlgorithm`.</span><span class="sxs-lookup"><span data-stu-id="6735c-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="6735c-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="6735c-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="6735c-153">Specifica l'algoritmo hash usato per calcolare l'impronta digitale del certificato.</span><span class="sxs-lookup"><span data-stu-id="6735c-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="6735c-154">Il valore predefinito è `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="6735c-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="6735c-155">I valori supportati sono `SHA256`, `SHA384` e `SHA512`</span><span class="sxs-lookup"><span data-stu-id="6735c-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="6735c-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="6735c-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="6735c-157">Specifica se il certificato per il firmatario attendibile deve essere concatenato a una radice non attendibile.</span><span class="sxs-lookup"><span data-stu-id="6735c-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="6735c-158">nome \<di NuGet Trusted-signers Remove-Name\></span><span class="sxs-lookup"><span data-stu-id="6735c-158">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="6735c-159">Rimuove eventuali firmatari attendibili che corrispondono al nome specificato.</span><span class="sxs-lookup"><span data-stu-id="6735c-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="6735c-160">nome \<sincronizzazione di NuGet Trusted-signers\></span><span class="sxs-lookup"><span data-stu-id="6735c-160">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="6735c-161">Richiede l'elenco più recente di certificati usati in un repository attualmente attendibile per aggiornare l'elenco di certificati esistente nel firmatario attendibile.</span><span class="sxs-lookup"><span data-stu-id="6735c-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="6735c-162">_Nota_: questo movimento eliminerà l'elenco corrente dei certificati e li sostituirà con un elenco aggiornato dal repository.</span><span class="sxs-lookup"><span data-stu-id="6735c-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="6735c-163">Opzioni</span><span class="sxs-lookup"><span data-stu-id="6735c-163">Options</span></span>

| <span data-ttu-id="6735c-164">Opzione</span><span class="sxs-lookup"><span data-stu-id="6735c-164">Option</span></span> | <span data-ttu-id="6735c-165">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6735c-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6735c-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="6735c-166">ConfigFile</span></span> | <span data-ttu-id="6735c-167">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="6735c-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6735c-168">Se non specificato, viene usato `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="6735c-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="6735c-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="6735c-169">ForceEnglishOutput</span></span> | <span data-ttu-id="6735c-170">Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese.</span><span class="sxs-lookup"><span data-stu-id="6735c-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="6735c-171">?</span><span class="sxs-lookup"><span data-stu-id="6735c-171">Help</span></span> | <span data-ttu-id="6735c-172">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="6735c-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="6735c-173">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="6735c-173">Verbosity</span></span> | <span data-ttu-id="6735c-174">Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*.</span><span class="sxs-lookup"><span data-stu-id="6735c-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="6735c-175">Esempi</span><span class="sxs-lookup"><span data-stu-id="6735c-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
