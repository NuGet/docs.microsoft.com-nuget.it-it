---
title: Comando per i firmatari dell'interfaccia della riga di comando di NuGet
description: Riferimento per il comando nuget.exe Trusted-signers
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9e25f439617a76d30880bea3c10a5d063e681a41
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238153"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="15631-103">comando Trusted-signers (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="15631-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="15631-104">**Si applica a:** versioni supportate per l'utilizzo di pacchetti &bullet; **:** 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="15631-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="15631-105">Ottiene o imposta i firmatari attendibili per la configurazione NuGet.</span><span class="sxs-lookup"><span data-stu-id="15631-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="15631-106">Per ulteriori informazioni sull'utilizzo, vedere [configurazioni comuni di NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="15631-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="15631-107">Per informazioni dettagliate sull'aspetto dello schema di nuget.config, vedere il [riferimento al file di configurazione NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="15631-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="15631-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="15631-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="15631-109">Se non `list|add|remove|sync` viene specificato alcun parametro, il comando utilizzerà per impostazione predefinita `list` .</span><span class="sxs-lookup"><span data-stu-id="15631-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="15631-110">elenco di firmatari attendibili NuGet</span><span class="sxs-lookup"><span data-stu-id="15631-110">nuget trusted-signers list</span></span>

<span data-ttu-id="15631-111">Elenca tutti i firmatari attendibili nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="15631-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="15631-112">Questa opzione includerà tutti i certificati (con algoritmo di impronta digitale e impronta digitale) di ogni firmatario.</span><span class="sxs-lookup"><span data-stu-id="15631-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="15631-113">Se un certificato ha un precedente `[U]` , significa che la voce del certificato è `allowUntrustedRoot` impostata come `true` .</span><span class="sxs-lookup"><span data-stu-id="15631-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="15631-114">Di seguito è riportato un esempio di output di questo comando:</span><span class="sxs-lookup"><span data-stu-id="15631-114">Below is an example output from this command:</span></span>

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
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="15631-115">NuGet Trusted-signers Add [opzioni]</span><span class="sxs-lookup"><span data-stu-id="15631-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="15631-116">Aggiunge al file di configurazione un firmatario attendibile con il nome specificato. Questa opzione ha movimenti diversi per aggiungere un autore o un repository attendibile.</span><span class="sxs-lookup"><span data-stu-id="15631-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="15631-117">Opzioni per l'aggiunta in base a un pacchetto</span><span class="sxs-lookup"><span data-stu-id="15631-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="15631-118">dove `<package(s)>` è uno o più `.nupkg` file.</span><span class="sxs-lookup"><span data-stu-id="15631-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

- **`-Author`**

  <span data-ttu-id="15631-119">Specifica che la firma dell'autore dei pacchetti deve essere attendibile.</span><span class="sxs-lookup"><span data-stu-id="15631-119">Specifies that the author signature of the package(s) should be trusted.</span></span>

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="15631-120">Specifica se il certificato per il firmatario attendibile deve essere concatenato a una radice non attendibile.</span><span class="sxs-lookup"><span data-stu-id="15631-120">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="15631-121">Elenco separato da punto e virgola di proprietari attendibili per limitare ulteriormente la relazione di trust di un repository.</span><span class="sxs-lookup"><span data-stu-id="15631-121">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="15631-122">Valido solo quando si usa l' `-Repository` opzione.</span><span class="sxs-lookup"><span data-stu-id="15631-122">Only valid when using the `-Repository` option.</span></span>

- **`-Repository`**

  <span data-ttu-id="15631-123">Specifica che la firma del repository o il controfirma dei pacchetti deve essere attendibile.</span><span class="sxs-lookup"><span data-stu-id="15631-123">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span>

<span data-ttu-id="15631-124">`-Author` `-Repository` Non è supportata la specifica di e allo stesso tempo.</span><span class="sxs-lookup"><span data-stu-id="15631-124">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="15631-125">Opzioni per l'aggiunta in base a un indice del servizio</span><span class="sxs-lookup"><span data-stu-id="15631-125">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="15631-126">_Nota_ : questa opzione consente di aggiungere solo repository attendibili.</span><span class="sxs-lookup"><span data-stu-id="15631-126">_Note_ : This option will only add trusted repositories.</span></span> 

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="15631-127">Specifica se il certificato per il firmatario attendibile deve essere concatenato a una radice non attendibile.</span><span class="sxs-lookup"><span data-stu-id="15631-127">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="15631-128">Elenco separato da punto e virgola di proprietari attendibili per limitare ulteriormente la relazione di trust di un repository.</span><span class="sxs-lookup"><span data-stu-id="15631-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span>

- **`-ServiceIndex`**

  <span data-ttu-id="15631-129">Specifica l'indice del servizio V3 del repository da ritenere attendibile.</span><span class="sxs-lookup"><span data-stu-id="15631-129">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="15631-130">Questo repository deve supportare la risorsa delle firme del repository.</span><span class="sxs-lookup"><span data-stu-id="15631-130">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="15631-131">Se non viene specificato, il comando cercherà un'origine del pacchetto con lo stesso `-Name` e otterrà l'indice del servizio.</span><span class="sxs-lookup"><span data-stu-id="15631-131">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span>

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="15631-132">Opzioni per l'aggiunta in base alle informazioni sul certificato</span><span class="sxs-lookup"><span data-stu-id="15631-132">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="15631-133">_Nota_ : se un firmatario attendibile con il nome specificato esiste già, l'elemento del certificato verrà aggiunto a tale firmatario.</span><span class="sxs-lookup"><span data-stu-id="15631-133">_Note_ : If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="15631-134">In caso contrario, verrà creato un autore attendibile con un elemento certificato fornito dalle informazioni del certificato.</span><span class="sxs-lookup"><span data-stu-id="15631-134">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>


- **`-AllowUntrustedRoot`**

  <span data-ttu-id="15631-135">Specifica se il certificato per il firmatario attendibile deve essere concatenato a una radice non attendibile.</span><span class="sxs-lookup"><span data-stu-id="15631-135">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="15631-136">Specifica le impronte digitali di un certificato con cui devono essere firmati i pacchetti firmati.</span><span class="sxs-lookup"><span data-stu-id="15631-136">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="15631-137">Un'impronta digitale del certificato è un hash del certificato.</span><span class="sxs-lookup"><span data-stu-id="15631-137">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="15631-138">L'algoritmo hash usato per il calcolo di questo hash deve essere specificato nell' `FingerprintAlgorithm` opzione.</span><span class="sxs-lookup"><span data-stu-id="15631-138">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span>

- **`-FingerprintAlgorithm`**

  <span data-ttu-id="15631-139">Specifica l'algoritmo hash usato per calcolare l'impronta digitale del certificato.</span><span class="sxs-lookup"><span data-stu-id="15631-139">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="15631-140">Il valore predefinito è `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="15631-140">Defaults to `SHA256`.</span></span> <span data-ttu-id="15631-141">I valori supportati sono `SHA256` , `SHA384` e `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="15631-141">Values supported are `SHA256`, `SHA384` and `SHA512`.</span></span>

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="15631-142">Nome attendibile-signers di NuGet \<name\></span><span class="sxs-lookup"><span data-stu-id="15631-142">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="15631-143">Rimuove eventuali firmatari attendibili che corrispondono al nome specificato.</span><span class="sxs-lookup"><span data-stu-id="15631-143">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="15631-144">Nome-sincronizzazione di NuGet Trusted-signers \<name\></span><span class="sxs-lookup"><span data-stu-id="15631-144">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="15631-145">Richiede l'elenco più recente di certificati usati in un repository attualmente attendibile per aggiornare l'elenco di certificati esistente nel firmatario attendibile.</span><span class="sxs-lookup"><span data-stu-id="15631-145">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="15631-146">_Nota_ : questo movimento eliminerà l'elenco corrente dei certificati e li sostituirà con un elenco aggiornato dal repository.</span><span class="sxs-lookup"><span data-stu-id="15631-146">_Note_ : This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="15631-147">Opzioni</span><span class="sxs-lookup"><span data-stu-id="15631-147">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="15631-148">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="15631-148">The NuGet configuration file to apply.</span></span> <span data-ttu-id="15631-149">Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="15631-149">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="15631-150">Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="15631-150">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="15631-151">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="15631-151">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="15631-152">Nome del firmatario attendibile.</span><span class="sxs-lookup"><span data-stu-id="15631-152">Name of the trusted signer.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="15631-153">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="15631-153">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="15631-154">Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="15631-154">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


## <a name="examples"></a><span data-ttu-id="15631-155">Esempi</span><span class="sxs-lookup"><span data-stu-id="15631-155">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
