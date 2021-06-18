---
title: Comando Di firma attendibile dell'interfaccia della riga di comando di NuGet
description: Informazioni di riferimento per il nuget.exe trusted signers
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: a5f3564af8b96dfa673d2252aea2e77a79c184a4
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323590"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="c7db0-103">Comando trusted-signers (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="c7db0-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="c7db0-104">**Si applica a:** Utilizzo pacchetti &bullet; **Versioni supportate:** 4.9.1+</span><span class="sxs-lookup"><span data-stu-id="c7db0-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="c7db0-105">Ottiene o imposta i firmatari attendibili per la configurazione NuGet.</span><span class="sxs-lookup"><span data-stu-id="c7db0-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="c7db0-106">Per un utilizzo aggiuntivo, vedere [Configurazioni NuGet comuni.](../../consume-packages/configuring-nuget-behavior.md)</span><span class="sxs-lookup"><span data-stu-id="c7db0-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="c7db0-107">Per informazioni dettagliate sull'aspetto nuget.config schema, vedere il riferimento al [file di configurazione NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="c7db0-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="c7db0-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="c7db0-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="c7db0-109">Se non viene specificato `list|add|remove|sync` nessuno di , il comando verrà utilizzato per impostazione `list` predefinita.</span><span class="sxs-lookup"><span data-stu-id="c7db0-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="c7db0-110">Elenco di firmatari attendibili nuget</span><span class="sxs-lookup"><span data-stu-id="c7db0-110">nuget trusted-signers list</span></span>

<span data-ttu-id="c7db0-111">Elenca tutti i firmatari attendibili nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="c7db0-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="c7db0-112">Questa opzione includerà tutti i certificati (con impronta digitale e algoritmo di impronta digitale) di ogni firmatario.</span><span class="sxs-lookup"><span data-stu-id="c7db0-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="c7db0-113">Se un certificato ha un precedente `[U]` , significa che la voce del certificato è `allowUntrustedRoot` impostata su `true` .</span><span class="sxs-lookup"><span data-stu-id="c7db0-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="c7db0-114">Di seguito è riportato un output di esempio di questo comando:</span><span class="sxs-lookup"><span data-stu-id="c7db0-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D
        SHA256 - 5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="c7db0-115">nuget trusted-signers add [options]</span><span class="sxs-lookup"><span data-stu-id="c7db0-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="c7db0-116">Aggiunge un firmatario attendibile con il nome specificato alla configurazione. Questa opzione ha movimenti diversi per aggiungere un autore o un repository attendibile.</span><span class="sxs-lookup"><span data-stu-id="c7db0-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="c7db0-117">Opzioni per l'aggiunta in base a un pacchetto</span><span class="sxs-lookup"><span data-stu-id="c7db0-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package> -Name <name> [options]
```

<span data-ttu-id="c7db0-118">dove `<package>` è un file `.nupkg` firmato.</span><span class="sxs-lookup"><span data-stu-id="c7db0-118">where `<package>` is one signed `.nupkg` file.</span></span>

- **`-Author`**

  <span data-ttu-id="c7db0-119">Specifica che la firma dell'autore del pacchetto firmato deve essere attendibile.</span><span class="sxs-lookup"><span data-stu-id="c7db0-119">Specifies that the author signature of the signed package should be trusted.</span></span>

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="c7db0-120">Specifica se il certificato per il firmatario attendibile deve essere autorizzato a concatenare a una radice non attendibile.</span><span class="sxs-lookup"><span data-stu-id="c7db0-120">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="c7db0-121">Elenco di proprietari attendibili separati da punto e virgola per limitare ulteriormente l'attendibilità di un repository.</span><span class="sxs-lookup"><span data-stu-id="c7db0-121">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="c7db0-122">Valido solo quando si usa `-Repository` l'opzione .</span><span class="sxs-lookup"><span data-stu-id="c7db0-122">Only valid when using the `-Repository` option.</span></span>

- **`-Repository`**

  <span data-ttu-id="c7db0-123">Specifica che la firma del repository o la controfirma del pacchetto firmato deve essere attendibile.</span><span class="sxs-lookup"><span data-stu-id="c7db0-123">Specifies that the repository signature or countersignature of the signed package should be trusted.</span></span>

<span data-ttu-id="c7db0-124">Non è supportato specificare sia che `-Author` `-Repository` contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="c7db0-124">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="c7db0-125">Opzioni per l'aggiunta in base a un indice del servizio</span><span class="sxs-lookup"><span data-stu-id="c7db0-125">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="c7db0-126">_Nota:_ questa opzione aggiungerà solo repository attendibili.</span><span class="sxs-lookup"><span data-stu-id="c7db0-126">_Note_: This option will only add trusted repositories.</span></span> 

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="c7db0-127">Specifica se il certificato per il firmatario attendibile deve essere autorizzato a concatenare a una radice non attendibile.</span><span class="sxs-lookup"><span data-stu-id="c7db0-127">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="c7db0-128">Elenco di proprietari attendibili separati da punto e virgola per limitare ulteriormente l'attendibilità di un repository.</span><span class="sxs-lookup"><span data-stu-id="c7db0-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span>

- **`-ServiceIndex`**

  <span data-ttu-id="c7db0-129">Specifica l'indice del servizio V3 del repository da considerato attendibile.</span><span class="sxs-lookup"><span data-stu-id="c7db0-129">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="c7db0-130">Questo repository deve supportare la risorsa firme del repository.</span><span class="sxs-lookup"><span data-stu-id="c7db0-130">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="c7db0-131">Se non viene specificato, il comando cerca un'origine del pacchetto con lo stesso `-Name` valore e ottiene l'indice del servizio da qui.</span><span class="sxs-lookup"><span data-stu-id="c7db0-131">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span>

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="c7db0-132">Opzioni per l'aggiunta in base alle informazioni sul certificato</span><span class="sxs-lookup"><span data-stu-id="c7db0-132">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="c7db0-133">_Nota:_ se esiste già un firmatario attendibile con il nome specificato, l'elemento del certificato verrà aggiunto a tale firmatario.</span><span class="sxs-lookup"><span data-stu-id="c7db0-133">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="c7db0-134">In caso contrario, verrà creato un autore attendibile con un elemento certificato dalle informazioni sul certificato specificato.</span><span class="sxs-lookup"><span data-stu-id="c7db0-134">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>


- **`-AllowUntrustedRoot`**

  <span data-ttu-id="c7db0-135">Specifica se il certificato per il firmatario attendibile deve essere autorizzato a concatenare a una radice non attendibile.</span><span class="sxs-lookup"><span data-stu-id="c7db0-135">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="c7db0-136">Specifica le impronte digitali di un certificato con cui devono essere firmati i pacchetti firmati.</span><span class="sxs-lookup"><span data-stu-id="c7db0-136">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="c7db0-137">Un'impronta digitale del certificato è un hash del certificato.</span><span class="sxs-lookup"><span data-stu-id="c7db0-137">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="c7db0-138">L'algoritmo hash usato per calcolare questo hash deve essere specificato `FingerprintAlgorithm` nell'opzione .</span><span class="sxs-lookup"><span data-stu-id="c7db0-138">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span>

- **`-FingerprintAlgorithm`**

  <span data-ttu-id="c7db0-139">Specifica l'algoritmo hash utilizzato per calcolare l'impronta digitale del certificato.</span><span class="sxs-lookup"><span data-stu-id="c7db0-139">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="c7db0-140">Il valore predefinito è `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="c7db0-140">Defaults to `SHA256`.</span></span> <span data-ttu-id="c7db0-141">I valori supportati `SHA256` sono , `SHA384` e `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="c7db0-141">Values supported are `SHA256`, `SHA384` and `SHA512`.</span></span>

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="c7db0-142">nuget trusted-signers remove -Name \<name\></span><span class="sxs-lookup"><span data-stu-id="c7db0-142">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="c7db0-143">Rimuove tutti i firmatari attendibili che corrispondono al nome specificato.</span><span class="sxs-lookup"><span data-stu-id="c7db0-143">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="c7db0-144">nuget trusted-signers sync -Name \<name\></span><span class="sxs-lookup"><span data-stu-id="c7db0-144">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="c7db0-145">Richiede l'elenco più recente dei certificati usati in un repository attualmente attendibile per aggiornare l'elenco di certificati esistente nel firmatario attendibile.</span><span class="sxs-lookup"><span data-stu-id="c7db0-145">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="c7db0-146">_Nota:_ questo movimento eliminerà l'elenco corrente di certificati e li sostituirà con un elenco aggiornato dal repository.</span><span class="sxs-lookup"><span data-stu-id="c7db0-146">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="c7db0-147">Opzioni</span><span class="sxs-lookup"><span data-stu-id="c7db0-147">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="c7db0-148">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="c7db0-148">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c7db0-149">Se non specificato, `%AppData%\NuGet\NuGet.Config` viene usato `~/.nuget/NuGet/NuGet.Config` (Windows) o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="c7db0-149">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="c7db0-150">Forza nuget.exe'esecuzione usando impostazioni cultura invarianti basate sull'inglese.</span><span class="sxs-lookup"><span data-stu-id="c7db0-150">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="c7db0-151">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="c7db0-151">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="c7db0-152">Nome del firmatario attendibile.</span><span class="sxs-lookup"><span data-stu-id="c7db0-152">Name of the trusted signer.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="c7db0-153">Elimina le richieste di input o di conferma dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c7db0-153">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="c7db0-154">Specifica la quantità di dettagli visualizzati nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="c7db0-154">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


## <a name="examples"></a><span data-ttu-id="c7db0-155">Esempi</span><span class="sxs-lookup"><span data-stu-id="c7db0-155">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget trusted-signers Remove -Name TrustedRepo

nuget trusted-signers Sync -Name TrustedRepo
```
