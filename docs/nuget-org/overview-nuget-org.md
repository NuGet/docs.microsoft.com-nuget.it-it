---
title: Panoramica di NuGet.org
description: Panoramica di NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427016"
---
# <a name="overview-of-nugetorg"></a><span data-ttu-id="a94b4-103">Panoramica di NuGet.org</span><span class="sxs-lookup"><span data-stu-id="a94b4-103">Overview of NuGet.org</span></span>

<span data-ttu-id="a94b4-104">NuGet.org è un host pubblico di pacchetti NuGet che vengono usati ogni giorno da milioni di sviluppatori .NET e .NET Core.</span><span class="sxs-lookup"><span data-stu-id="a94b4-104">NuGet.org is a public host of NuGet packages that are employed by millions of .NET and .NET Core developers every day.</span></span>

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a><span data-ttu-id="a94b4-105">Ruolo di NuGet.org nell'ecosistema NuGet</span><span class="sxs-lookup"><span data-stu-id="a94b4-105">Role of NuGet.org in the NuGet ecosystem</span></span>

<span data-ttu-id="a94b4-106">Come host pubblico, NuGet.org gestisce il repository centrale di oltre 100.000 pacchetti univoci su [nuget.org](https://www.nuget.org). NuGet.org non è l'unico host possibile per i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="a94b4-106">In its role as a public host, NuGet.org itself maintains the central repository of over 100,000 unique packages at [nuget.org](https://www.nuget.org). NuGet.org is not the only possible host for packages.</span></span> <span data-ttu-id="a94b4-107">La tecnologia NuGet consente anche di ospitare i pacchetti in modo privato nel cloud (ad esempio in Azure DevOps), in una rete privata o anche direttamente nel file system locale.</span><span class="sxs-lookup"><span data-stu-id="a94b4-107">The NuGet technology also enables you to host packages privately in the cloud (such as on Azure DevOps), on a private network, or even on just your local file system.</span></span> <span data-ttu-id="a94b4-108">Se è interessati a un host diverso o a un'opzione di hosting diversa, vedere [Hosting dei feed NuGet](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="a94b4-108">If you are interested in a different host or hosting option, see [Hosting your own NuGet feeds](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="a94b4-109">Come qualsiasi host di pacchetti NuGet, NuGet.org fa da punto di connessione tra gli *autori* e i *consumer* dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="a94b4-109">NuGet.org, like any host for NuGet packages, serves as the point of connection between package *creators* and package *consumers*.</span></span> <span data-ttu-id="a94b4-110">Gli autori compilano utili pacchetti NuGet e li pubblicano.</span><span class="sxs-lookup"><span data-stu-id="a94b4-110">Creators build useful NuGet packages and publish them.</span></span> <span data-ttu-id="a94b4-111">I consumer cercano quindi i pacchetti utili e compatibili negli host accessibili, scaricandoli e includendoli nei loro progetti.</span><span class="sxs-lookup"><span data-stu-id="a94b4-111">Consumers then search for useful and compatible packages on accessible hosts, downloading and including those packages in their projects.</span></span> <span data-ttu-id="a94b4-112">Una volta installate in un progetto, le API dei pacchetti sono disponibili per il resto del codice del progetto.</span><span class="sxs-lookup"><span data-stu-id="a94b4-112">Once installed in a project, the packages' APIs are available to the rest of the project code.</span></span>

![Relazione tra autori, host e consumer dei pacchetti](media/nuget-roles.png)

## <a name="accounts"></a><span data-ttu-id="a94b4-114">Account</span><span class="sxs-lookup"><span data-stu-id="a94b4-114">Accounts</span></span>

<span data-ttu-id="a94b4-115">Per pubblicare pacchetti in NuGet.org, iniziare creando un [account individuale (account utente)](individual-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="a94b4-115">To publish packages on NuGet.org, you first create an [individual (user) account](individual-accounts.md).</span></span> <span data-ttu-id="a94b4-116">Questo account diventa l'identità dell'utente in NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="a94b4-116">This becomes your identity on NuGet.org.</span></span>

<span data-ttu-id="a94b4-117">NuGet.org consente anche di creare un [account aziendale](organizations-on-nuget-org.md).</span><span class="sxs-lookup"><span data-stu-id="a94b4-117">NuGet.org also allows you to create an [organization account](organizations-on-nuget-org.md).</span></span> <span data-ttu-id="a94b4-118">Un account aziendale ha uno o più account individuali come membri.</span><span class="sxs-lookup"><span data-stu-id="a94b4-118">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="a94b4-119">I membri possono gestire un set di pacchetti mantenendo un'unica identità per la proprietà.</span><span class="sxs-lookup"><span data-stu-id="a94b4-119">Members can manage a set of packages while maintaining a single identity for ownership.</span></span> <span data-ttu-id="a94b4-120">L'account personale consente a un utente di essere membro di un numero qualsiasi di organizzazioni.</span><span class="sxs-lookup"><span data-stu-id="a94b4-120">Through your individual account, you can be a member of any number of organizations.</span></span>

<span data-ttu-id="a94b4-121">Un pacchetto può appartenere a un account aziendale come a un account individuale.</span><span class="sxs-lookup"><span data-stu-id="a94b4-121">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="a94b4-122">I consumer di pacchetti non vedono alcuna differenza tra un account individuale e l'account aziendale: entrambi vengono visualizzati come `owners` (proprietari) del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a94b4-122">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="api-keys"></a><span data-ttu-id="a94b4-123">Chiavi API</span><span class="sxs-lookup"><span data-stu-id="a94b4-123">API keys</span></span>

<span data-ttu-id="a94b4-124">Dopo aver creato un pacchetto NuGet (un file con estensione *nupkg*) da pubblicare, pubblicarlo in NuGet.org usando l'interfaccia della riga di comando nuget.exe o dotnet.exe insieme a una [chiave API](scoped-api-keys.md) acquisita da NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="a94b4-124">Once you have a NuGet package (*.nupkg* file) to publish, you publish it to NuGet.org using either the nuget.exe CLI or the dotnet.exe CLI, along with an [API key](scoped-api-keys.md) acquired from NuGet.org.</span></span>

<span data-ttu-id="a94b4-125">Quando si [pubblica un pacchetto](../create-packages/creating-a-package.md), si include il valore della chiave API nel comando dell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="a94b4-125">When you [publish a package](../create-packages/creating-a-package.md), you include the API key value in the CLI command.</span></span>

## <a name="id-prefixes"></a><span data-ttu-id="a94b4-126">Prefissi ID</span><span class="sxs-lookup"><span data-stu-id="a94b4-126">ID prefixes</span></span>

<span data-ttu-id="a94b4-127">Quando si esegue la pubblicazione dei pacchetti, è possibile riservare e proteggere la propria identità [riservando prefissi ID](id-prefix-reservation.md).</span><span class="sxs-lookup"><span data-stu-id="a94b4-127">When you publish packages, you can reserve and protect your identity by [reserving ID prefixes](id-prefix-reservation.md).</span></span> <span data-ttu-id="a94b4-128">Quando si installa un pacchetto, ai consumer di pacchetti vengono fornite informazioni aggiuntive indicanti che le proprietà di identificazione del pacchetto in uso non sono fuorvianti.</span><span class="sxs-lookup"><span data-stu-id="a94b4-128">When installing a package, package consumers are provided with additional information indicating that the package they are consuming is not deceptive in its identifying properties.</span></span>

## <a name="api-endpoint-for-nugetorg"></a><span data-ttu-id="a94b4-129">Endpoint API per NuGet.org</span><span class="sxs-lookup"><span data-stu-id="a94b4-129">API endpoint for NuGet.org</span></span>

<span data-ttu-id="a94b4-130">Per usare NuGet.org come repository di pacchetti con i client NuGet, è consigliabile usare l'endpoint API V3 seguente:</span><span class="sxs-lookup"><span data-stu-id="a94b4-130">To use NuGet.org as a package repository with NuGet clients, you should use the following V3 API endpoint:</span></span> 

`https://api.nuget.org/v3/index.json`

<span data-ttu-id="a94b4-131">I client meno recenti possono comunque usare il protocollo V2 per raggiungere NuGet.org. Si noti tuttavia che i client NuGet 3.0 o versione successiva avranno un servizio più lento e meno affidabile se usano il protocollo V2:</span><span class="sxs-lookup"><span data-stu-id="a94b4-131">Older clients can still use the V2 protocol to reach NuGet.org. However, please note, NuGet clients 3.0 or later will have slower and less reliable service using the V2 protocol:</span></span>

<span data-ttu-id="a94b4-132">`https://www.nuget.org/api/v2` (**il protocollo V2 è deprecato.** )</span><span class="sxs-lookup"><span data-stu-id="a94b4-132">`https://www.nuget.org/api/v2` (**The V2 prototcol is deprecated!**)</span></span>
