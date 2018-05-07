---
title: Firma di pacchetti NuGet
description: Informazioni su come è possibile usare pacchetti firmati per abilitare la verifica dell'integrità del contenuto.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a469cbdd218a0e9c18950bb0d36faf4dbcb42a01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="d94db-103">Firma di pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="d94db-103">Signing NuGet Packages</span></span>

<span data-ttu-id="d94db-104">La firma di un pacchetto è un processo per assicurarsi che il pacchetto non sia stato modificato dopo la creazione.</span><span class="sxs-lookup"><span data-stu-id="d94db-104">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d94db-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d94db-105">Prerequisites</span></span>

1. <span data-ttu-id="d94db-106">Il pacchetto (file `.nupkg`) da firmare.</span><span class="sxs-lookup"><span data-stu-id="d94db-106">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="d94db-107">Vedere [Creazione di un pacchetto](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="d94db-107">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="d94db-108">nuget.exe 4.6.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="d94db-108">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="d94db-109">Vedere come [installare l'interfaccia della riga di comando di nuget.exe](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="d94db-109">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="d94db-110">[Un certificato di firma del codice](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span><span class="sxs-lookup"><span data-stu-id="d94db-110">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

> [!Warning]
> <span data-ttu-id="d94db-111">nuget.org non accetta attualmente pacchetti firmati.</span><span class="sxs-lookup"><span data-stu-id="d94db-111">nuget.org does not currently accept signed packages.</span></span> <span data-ttu-id="d94db-112">È possibile firmare pacchetti per la pubblicazione in feed personalizzati.</span><span class="sxs-lookup"><span data-stu-id="d94db-112">You can sign packages for publishing to custom feeds.</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="d94db-113">Firmare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="d94db-113">Sign a package</span></span>

<span data-ttu-id="d94db-114">Per firmare un pacchetto, usare [nuget sign](../tools/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="d94db-114">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="d94db-115">Come descritto nelle informazioni di riferimento sui comandi, è possibile usare un certificato disponibile nell'archivio certificati o usare un certificato da un file.</span><span class="sxs-lookup"><span data-stu-id="d94db-115">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="d94db-116">Problemi comuni durante la firma di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="d94db-116">Common problems when signing a package</span></span>

- <span data-ttu-id="d94db-117">Il certificato non è valido per la firma del codice.</span><span class="sxs-lookup"><span data-stu-id="d94db-117">The certificate is not valid for code signing.</span></span> <span data-ttu-id="d94db-118">È necessario assicurarsi che il certificato specificato abbia l'utilizzo chiavi avanzato appropriato (EKU 1.3.6.1.5.5.7.3.3).</span><span class="sxs-lookup"><span data-stu-id="d94db-118">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="d94db-119">Il certificato non soddisfa i requisiti di base, ad esempio l'algoritmo di firma RSA SHA-256 o una chiave pubblica a 2048 bit o superiore.</span><span class="sxs-lookup"><span data-stu-id="d94db-119">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="d94db-120">Il certificato è scaduto o è stato revocato.</span><span class="sxs-lookup"><span data-stu-id="d94db-120">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="d94db-121">Il server di timestamp non soddisfa i requisiti del certificato.</span><span class="sxs-lookup"><span data-stu-id="d94db-121">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="d94db-122">I pacchetti firmati devono includere un timestamp per assicurarsi che la firma rimanga valida dopo la scadenza del certificato di firma.</span><span class="sxs-lookup"><span data-stu-id="d94db-122">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="d94db-123">L'operazione di firma genera un [avviso NU3002](../reference/Errors-and-Warnings.md#nu3002) se avviene senza un timestamp.</span><span class="sxs-lookup"><span data-stu-id="d94db-123">The sign operation produce a [warning NU3002](../reference/Errors-and-Warnings.md#nu3002) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="d94db-124">Verificare un pacchetto firmato</span><span class="sxs-lookup"><span data-stu-id="d94db-124">Verify a signed package</span></span>

<span data-ttu-id="d94db-125">Usare [nuget verify](../tools/cli-ref-verify.md) per visualizzare i dettagli di firma di un determinato pacchetto:</span><span class="sxs-lookup"><span data-stu-id="d94db-125">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="d94db-126">Installare un pacchetto firmato</span><span class="sxs-lookup"><span data-stu-id="d94db-126">Install a signed package</span></span>

<span data-ttu-id="d94db-127">Non sono richieste azioni specifiche per l'installazione di pacchetti firmati. Tuttavia, se il contenuto è stato modificato dopo la firma, l'installazione viene bloccata e genera un [errore NU3008](../reference/Errors-and-Warnings.md#nu3008).</span><span class="sxs-lookup"><span data-stu-id="d94db-127">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span></span>

> [!Warning]
> <span data-ttu-id="d94db-128">I pacchetti firmati con certificati non attendibili vengono considerati non firmati e installati senza eventuali avvisi o errori come qualsiasi altro pacchetto non firmato.</span><span class="sxs-lookup"><span data-stu-id="d94db-128">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="d94db-129">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d94db-129">See also</span></span>

[<span data-ttu-id="d94db-130">Informazioni di riferimento sui pacchetti firmati</span><span class="sxs-lookup"><span data-stu-id="d94db-130">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
