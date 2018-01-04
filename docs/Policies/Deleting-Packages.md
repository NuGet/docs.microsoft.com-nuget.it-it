---
title: Eliminazione di pacchetti NuGet da nuget.org | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a348ca2e-0a5d-40ad-ba33-9bb37e1d980b
description: "Criteri per la rimozione di pacchetti dall'elenco di nuget.org; l'eliminazione permanente non è supportata, salvo quando i pacchetti violano altri criteri."
keywords: Eliminazione di pacchetti NuGet, rimozione di pacchetti NuGet dall'elenco, usi non consentiti dei pacchetti
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 331979bdc3703ddbeff18e2bd0e6b0a17551e68b
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="deleting-packages"></a><span data-ttu-id="1d0fa-104">Eliminazione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="1d0fa-104">Deleting packages</span></span>

<span data-ttu-id="1d0fa-105">nuget.org non supporta l'eliminazione permanente dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="1d0fa-105">nuget.org does not support permanent deletion of packages.</span></span> <span data-ttu-id="1d0fa-106">Questa operazione comporterebbe l'interruzione di tutti i progetti che dipendono dalla disponibilità del pacchetto eliminato, in particolare con i flussi di lavoro di compilazione che implicano il ripristino del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1d0fa-106">Doing so would break every project depending on the availability of the package, especially with build workflows that involve package restore.</span></span>

<span data-ttu-id="1d0fa-107">nuget.org supporta invece la *rimozione dall'elenco* di un pacchetto, che può essere eseguita nella pagina di gestione del pacchetto nel sito Web.</span><span class="sxs-lookup"><span data-stu-id="1d0fa-107">nuget.org does supports *unlisting* a package, which can be done in the package management page on the web site.</span></span> <span data-ttu-id="1d0fa-108">I pacchetti rimossi dall'elenco non vengono visualizzati su nuget.org o nell'interfaccia utente di Visual Studio, né compaiono all'interno dei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="1d0fa-108">Unlisted packages don't appear on nuget.org or in the Visual Studio UI, and do not appear in search results.</span></span> <span data-ttu-id="1d0fa-109">I pacchetti rimossi dall'elenco, tuttavia, possono essere ancora scaricati e installati usando il numero di versione esatto, che supporta il ripristino del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1d0fa-109">Unlisted packages, however, can still be downloaded and installed by using an exact version number, which supports package restore.</span></span> <span data-ttu-id="1d0fa-110">Inoltre, i pacchetti rimossi dall'elenco potrebbero essere ancora individuati negli scenari specifici seguenti:</span><span class="sxs-lookup"><span data-stu-id="1d0fa-110">In addition, unlisted packages may still be discovered in the following specific scenarios:</span></span>

- <span data-ttu-id="1d0fa-111">Ripristino del pacchetto usando versioni mobili (ad esempio, `1.0.0-*`), se il pacchetto più recente disponibile corrispondente alle limitazioni della versione o della dipendenza è un pacchetto rimosso dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="1d0fa-111">Package restore using floating versions (for example, `1.0.0-*`), if the latest available package matching the version or dependency constraints is an unlisted package.</span></span>
- <span data-ttu-id="1d0fa-112">Replica dei pacchetti tramite il catalogo (dal momento che il catalogo contiene anche pacchetti rimossi dall'elenco).</span><span class="sxs-lookup"><span data-stu-id="1d0fa-112">Replication of packages through the catalog (as the catalog also contains unlisted packages).</span></span>

## <a name="exceptions"></a><span data-ttu-id="1d0fa-113">Eccezioni</span><span class="sxs-lookup"><span data-stu-id="1d0fa-113">Exceptions</span></span>

<span data-ttu-id="1d0fa-114">In situazioni eccezionali, quali violazione del copyright e contenuto potenzialmente dannoso, i pacchetti possono essere eliminati manualmente dal team di NuGet.</span><span class="sxs-lookup"><span data-stu-id="1d0fa-114">In exceptional situations such as copyright infringement and potentially harmful content, packages can be deleted manually by the NuGet team.</span></span> <span data-ttu-id="1d0fa-115">Inviare una richiesta di supporto tramite la [raccolta NuGet](http://www.nuget.org) per avviare il processo.</span><span class="sxs-lookup"><span data-stu-id="1d0fa-115">Submit a support request through [NuGet Gallery](http://www.nuget.org) to start the process.</span></span>

## <a name="prohibited-use"></a><span data-ttu-id="1d0fa-116">Uso non consentito</span><span class="sxs-lookup"><span data-stu-id="1d0fa-116">Prohibited use</span></span>

<span data-ttu-id="1d0fa-117">I pacchetti che soddisfano uno dei criteri seguenti non sono consentiti nella raccolta NuGet pubblica e verranno immediatamente rimossi senza discussione.</span><span class="sxs-lookup"><span data-stu-id="1d0fa-117">Packages that meet any of the following criteria are not allowed on the public NuGet gallery and will be immediately removed without discussion.</span></span> <span data-ttu-id="1d0fa-118">I proprietari dei pacchetti verranno tuttavia informati della rimozione.</span><span class="sxs-lookup"><span data-stu-id="1d0fa-118">Package owners will, however, be notified of the removal.</span></span>

- <span data-ttu-id="1d0fa-119">Contengono malware, adware o qualsiasi tipo di spyware.</span><span class="sxs-lookup"><span data-stu-id="1d0fa-119">Contains malware, adware, or any kind of spyware.</span></span>
- <span data-ttu-id="1d0fa-120">Sono progettati per danneggiare la workstation dello sviluppatore o l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="1d0fa-120">Are designed to harm a developer's workstation or their organization.</span></span>
- <span data-ttu-id="1d0fa-121">Violano diritti di copyright o licenze.</span><span class="sxs-lookup"><span data-stu-id="1d0fa-121">Infringes copyrights or violates licenses.</span></span>
- <span data-ttu-id="1d0fa-122">Contengono contenuto illecito.</span><span class="sxs-lookup"><span data-stu-id="1d0fa-122">Contains illegal content.</span></span>
- <span data-ttu-id="1d0fa-123">Vengono usati per appropriarsi degli identificatori dei pacchetti, inclusi i pacchetti che hanno un contenuto produttivo nullo.</span><span class="sxs-lookup"><span data-stu-id="1d0fa-123">Are being used to squat on package identifiers, including packages that have zero productive content.</span></span> <span data-ttu-id="1d0fa-124">I pacchetti devono contenere codice oppure i proprietari devono concedere l'identificatore a un utente che abbia effettivamente un prodotto da fornire.</span><span class="sxs-lookup"><span data-stu-id="1d0fa-124">Packages must contain code or the owners must concede the identifier to someone who actually has a product to ship.</span></span>
- <span data-ttu-id="1d0fa-125">Tentano di fare in modo che la raccolta esegua operazioni per cui non è stata esplicitamente progettata.</span><span class="sxs-lookup"><span data-stu-id="1d0fa-125">Attempt to make the gallery do something that it is not explicitly designed to do.</span></span>

<span data-ttu-id="1d0fa-126">Se si trova un pacchetto che è palesemente in violazione di una di queste condizioni, fare clic sul collegamento **Report Abuse** (Segnala abusi) nella pagina dei dettagli del pacchetto e inviare un report.</span><span class="sxs-lookup"><span data-stu-id="1d0fa-126">If you find a package that is in violation of any of these items, click the **Report Abuse** link on the package details page and submit a report.</span></span>

<span data-ttu-id="1d0fa-127">Si noti che il team di NuGet e .NET Foundation si riservano il diritto di modificare questi criteri in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="1d0fa-127">Note that the NuGet team and the .NET Foundation reserves the right to change these criteria at any time.</span></span>
