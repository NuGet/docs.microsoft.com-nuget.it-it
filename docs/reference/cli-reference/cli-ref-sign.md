---
title: Comando firma CLI NuGet
description: Riferimento per il comando nuget.exe Sign
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622772"
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="33f71-103">comando Sign (interfaccia della riga di comando NuGet)</span><span class="sxs-lookup"><span data-stu-id="33f71-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="33f71-104">**Si applica a:** versioni supportate per la creazione di pacchetti &bullet; **:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="33f71-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="33f71-105">Firma tutti i pacchetti che corrispondono al primo argomento con un certificato.</span><span class="sxs-lookup"><span data-stu-id="33f71-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="33f71-106">Il certificato con la chiave privata può essere ottenuto da un file o da un certificato installato in un archivio certificati fornendo un nome soggetto o un'identificazione personale.</span><span class="sxs-lookup"><span data-stu-id="33f71-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

> [!Note]
> <span data-ttu-id="33f71-107">La firma del pacchetto non è ancora supportata in .NET Core, in mono o in piattaforme non Windows.</span><span class="sxs-lookup"><span data-stu-id="33f71-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="33f71-108">Uso</span><span class="sxs-lookup"><span data-stu-id="33f71-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="33f71-109">dove `<package(s)>` è uno o più `.nupkg` file.</span><span class="sxs-lookup"><span data-stu-id="33f71-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="33f71-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="33f71-110">Options</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="33f71-111">Specifica l'impronta digitale SHA-1 del certificato utilizzato per eseguire la ricerca in un archivio certificati locale per il certificato.</span><span class="sxs-lookup"><span data-stu-id="33f71-111">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span>

- **`-CertificatePassword`**

  <span data-ttu-id="33f71-112">Specifica la password del certificato, se necessario.</span><span class="sxs-lookup"><span data-stu-id="33f71-112">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="33f71-113">Se un certificato è protetto da password ma non viene fornita alcuna password, il comando richiederà una password in fase di esecuzione, a meno che non `-NonInteractive` venga passata l'opzione.</span><span class="sxs-lookup"><span data-stu-id="33f71-113">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the `-NonInteractive` option is passed.</span></span>

- **`-CertificatePath`**

  <span data-ttu-id="33f71-114">Specifica il percorso del file del certificato da utilizzare per la firma del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="33f71-114">Specifies the file path to the certificate to be used in signing the package.</span></span>

- **`-CertificateStoreLocation`**

  <span data-ttu-id="33f71-115">Specifica il nome dell'archivio certificati X. 509 utilizzato per cercare il certificato.</span><span class="sxs-lookup"><span data-stu-id="33f71-115">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="33f71-116">Il valore predefinito è "CurrentUser", l'archivio certificati X. 509 utilizzato dall'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="33f71-116">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="33f71-117">Questa opzione deve essere usata quando si specifica il certificato tramite le `-CertificateSubjectName` `-CertificateFingerprint` Opzioni o.</span><span class="sxs-lookup"><span data-stu-id="33f71-117">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateStoreName`**

  <span data-ttu-id="33f71-118">Specifica il nome dell'archivio certificati X. 509 da utilizzare per la ricerca del certificato.</span><span class="sxs-lookup"><span data-stu-id="33f71-118">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="33f71-119">Il valore predefinito è "My", l'archivio certificati X. 509 per i certificati personali.</span><span class="sxs-lookup"><span data-stu-id="33f71-119">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="33f71-120">Questa opzione deve essere usata quando si specifica il certificato tramite le `-CertificateSubjectName` `-CertificateFingerprint` Opzioni o.</span><span class="sxs-lookup"><span data-stu-id="33f71-120">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateSubjectName`**

  <span data-ttu-id="33f71-121">Specifica il nome del soggetto del certificato utilizzato per eseguire la ricerca in un archivio certificati locale per il certificato.</span><span class="sxs-lookup"><span data-stu-id="33f71-121">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="33f71-122">La ricerca è un confronto tra stringhe senza distinzione tra maiuscole e minuscole usando il valore fornito, che troverà tutti i certificati con il nome del soggetto che contiene tale stringa, indipendentemente dagli altri valori dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="33f71-122">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="33f71-123">L'archivio certificati può essere specificato dalle `-CertificateStoreName` `-CertificateStoreLocation` Opzioni e.</span><span class="sxs-lookup"><span data-stu-id="33f71-123">The certificate store can be specified by `-CertificateStoreName` and `-CertificateStoreLocation` options.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="33f71-124">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="33f71-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="33f71-125">Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="33f71-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="33f71-126">Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="33f71-126">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-HashAlgorithm`**

  <span data-ttu-id="33f71-127">Algoritmo hash da utilizzare per firmare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="33f71-127">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="33f71-128">Il valore predefinito è SHA256.</span><span class="sxs-lookup"><span data-stu-id="33f71-128">Defaults to SHA256.</span></span> <span data-ttu-id="33f71-129">I valori possibili sono SHA256, SHA384 e SHA512.</span><span class="sxs-lookup"><span data-stu-id="33f71-129">Possible values are SHA256, SHA384, and SHA512.</span></span>

- **`-?|-help`**

  <span data-ttu-id="33f71-130">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="33f71-130">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="33f71-131">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="33f71-131">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="33f71-132">Specifica la directory in cui deve essere salvato il pacchetto firmato.</span><span class="sxs-lookup"><span data-stu-id="33f71-132">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="33f71-133">Per impostazione predefinita, il pacchetto originale viene sovrascritto dal pacchetto firmato.</span><span class="sxs-lookup"><span data-stu-id="33f71-133">By default the original package is overwritten by the signed package.</span></span>

- **`-Overwrite`**

  <span data-ttu-id="33f71-134">Opzione per indicare se la firma corrente deve essere sovrascritta.</span><span class="sxs-lookup"><span data-stu-id="33f71-134">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="33f71-135">Per impostazione predefinita, il comando avrà esito negativo se il pacchetto dispone già di una firma.</span><span class="sxs-lookup"><span data-stu-id="33f71-135">By default the command will fail if the package already has a signature.</span></span>

- **`-Timestamper`**

  <span data-ttu-id="33f71-136">URL di un server di timestamp RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="33f71-136">URL to an RFC 3161 timestamping server.</span></span>

- **`-TimestampHashAlgorithm`**

  <span data-ttu-id="33f71-137">Algoritmo hash che verrà usato dal server di timestamp RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="33f71-137">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="33f71-138">Il valore predefinito è SHA256.</span><span class="sxs-lookup"><span data-stu-id="33f71-138">Defaults to SHA256.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="33f71-139">Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="33f71-139">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="33f71-140">Esempi</span><span class="sxs-lookup"><span data-stu-id="33f71-140">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
