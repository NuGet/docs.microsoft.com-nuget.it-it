---
title: Firma di pacchetti NuGet
description: Informazioni su come è possibile usare pacchetti firmati per abilitare la verifica dell'integrità del contenuto.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 9900db1970a89de129d9074e5900e0aa048101de
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2018
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="9fcfa-103">Firma di pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="9fcfa-103">Signing NuGet Packages</span></span>

<span data-ttu-id="9fcfa-104">La firma di un pacchetto è un processo per assicurarsi che il pacchetto non sia stato modificato dopo la creazione.</span><span class="sxs-lookup"><span data-stu-id="9fcfa-104">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fcfa-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9fcfa-105">Prerequisites</span></span>

1. <span data-ttu-id="9fcfa-106">Il pacchetto (file `.nupkg`) da firmare.</span><span class="sxs-lookup"><span data-stu-id="9fcfa-106">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="9fcfa-107">Vedere [Creazione di un pacchetto](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="9fcfa-107">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="9fcfa-108">nuget.exe 4.6.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="9fcfa-108">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="9fcfa-109">Vedere come [installare l'interfaccia della riga di comando di nuget.exe](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="9fcfa-109">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="9fcfa-110">[Un certificato di firma del codice](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span><span class="sxs-lookup"><span data-stu-id="9fcfa-110">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="9fcfa-111">Firmare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="9fcfa-111">Sign a package</span></span>

<span data-ttu-id="9fcfa-112">Per firmare un pacchetto, usare [nuget sign](../tools/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="9fcfa-112">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="9fcfa-113">Come descritto nelle informazioni di riferimento sui comandi, è possibile usare un certificato disponibile nell'archivio certificati o usare un certificato da un file.</span><span class="sxs-lookup"><span data-stu-id="9fcfa-113">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="9fcfa-114">Problemi comuni durante la firma di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="9fcfa-114">Common problems when signing a package</span></span>

- <span data-ttu-id="9fcfa-115">Il certificato non è valido per la firma del codice.</span><span class="sxs-lookup"><span data-stu-id="9fcfa-115">The certificate is not valid for code signing.</span></span> <span data-ttu-id="9fcfa-116">È necessario assicurarsi che il certificato specificato abbia l'utilizzo chiavi avanzato appropriato (EKU 1.3.6.1.5.5.7.3.3).</span><span class="sxs-lookup"><span data-stu-id="9fcfa-116">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="9fcfa-117">Il certificato non soddisfa i requisiti di base, ad esempio l'algoritmo di firma RSA SHA-256 o una chiave pubblica a 2048 bit o superiore.</span><span class="sxs-lookup"><span data-stu-id="9fcfa-117">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="9fcfa-118">Il certificato è scaduto o è stato revocato.</span><span class="sxs-lookup"><span data-stu-id="9fcfa-118">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="9fcfa-119">Il server di timestamp non soddisfa i requisiti del certificato.</span><span class="sxs-lookup"><span data-stu-id="9fcfa-119">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="9fcfa-120">I pacchetti firmati devono includere un timestamp per assicurarsi che la firma rimanga valida dopo la scadenza del certificato di firma.</span><span class="sxs-lookup"><span data-stu-id="9fcfa-120">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="9fcfa-121">L'operazione di firma genera un [avviso NU3002](../reference/Errors-and-Warnings.md#nu3002) se avviene senza un timestamp.</span><span class="sxs-lookup"><span data-stu-id="9fcfa-121">The sign operation produce a [warning NU3002](../reference/Errors-and-Warnings.md#nu3002) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="9fcfa-122">Verificare un pacchetto firmato</span><span class="sxs-lookup"><span data-stu-id="9fcfa-122">Verify a signed package</span></span>

<span data-ttu-id="9fcfa-123">Usare [nuget verify](../tools/cli-ref-verify.md) per visualizzare i dettagli di firma di un determinato pacchetto:</span><span class="sxs-lookup"><span data-stu-id="9fcfa-123">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="9fcfa-124">Installare un pacchetto firmato</span><span class="sxs-lookup"><span data-stu-id="9fcfa-124">Install a signed package</span></span>

<span data-ttu-id="9fcfa-125">Non sono richieste azioni specifiche per l'installazione di pacchetti firmati. Tuttavia, se il contenuto è stato modificato dopo la firma, l'installazione viene bloccata e genera un [errore NU3008](../reference/Errors-and-Warnings.md#nu3008).</span><span class="sxs-lookup"><span data-stu-id="9fcfa-125">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span></span>

> [!Warning]
> <span data-ttu-id="9fcfa-126">I pacchetti firmati con certificati non attendibili vengono considerati non firmati e installati senza eventuali avvisi o errori come qualsiasi altro pacchetto non firmato.</span><span class="sxs-lookup"><span data-stu-id="9fcfa-126">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="9fcfa-127">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9fcfa-127">See also</span></span>

[<span data-ttu-id="9fcfa-128">Informazioni di riferimento sui pacchetti firmati</span><span class="sxs-lookup"><span data-stu-id="9fcfa-128">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
