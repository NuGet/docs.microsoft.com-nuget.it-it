---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 717cf8c47335c620410be71300b07de82799e1d3
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427116"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="12acd-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="12acd-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="12acd-103">Spiegazione logica:</span><span class="sxs-lookup"><span data-stu-id="12acd-103">Rationale</span></span>

<span data-ttu-id="12acd-104">Con l'introduzione delle [espressioni di licenza](../reference/nuspec.md#license), è nata l'esigenza di avere un servizio affidabile che specificasse un testo di riferimento per ogni identificatore di licenza, identificatore di eccezione o espressione di licenza.</span><span class="sxs-lookup"><span data-stu-id="12acd-104">With the introduction of the [license expressions](../reference/nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="12acd-105">Un requisito aggiuntivo per questo servizio è la necessità di uno schema URL stabile, che non sia soggetto alla rottura dei collegamenti, ma che possa invece essere usato in modo sicuro per assicurare ai client meno recenti compatibilità con le versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="12acd-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="12acd-106">Licenses.NuGet.org è il servizio adatto.</span><span class="sxs-lookup"><span data-stu-id="12acd-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="12acd-107">Viene usato da Nuget.org per creare il riferimento di testo della licenza per i pacchetti che specificano la licenza usando un'espressione di licenza.</span><span class="sxs-lookup"><span data-stu-id="12acd-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="12acd-108">Con il comando `nuget pack` o la compressione di altri [strumenti client](../install-nuget-client-tools.md) si imposta l'elemento [`licenseUrl`](../reference/nuspec.md#licenseurl) in modo che faccia riferimento a licenses.nuget.org to per assicurare compatibilità con le versioni precedenti ai client meno recenti che non supportano l'elemento `license`.</span><span class="sxs-lookup"><span data-stu-id="12acd-108">`nuget pack` or packing with other [client tools](../install-nuget-client-tools.md) set the [`licenseUrl`](../reference/nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="12acd-109">Protocollo</span><span class="sxs-lookup"><span data-stu-id="12acd-109">Protocol</span></span>

<span data-ttu-id="12acd-110">Licenses.nuget.org è destinato a essere visualizzato dagli utenti nei browser. Non sono previste risposte leggibili al computer.</span><span class="sxs-lookup"><span data-stu-id="12acd-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="12acd-111">È necessario usare il protocollo HTTPS e le richieste devono essere costruite in un modo specifico.</span><span class="sxs-lookup"><span data-stu-id="12acd-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="12acd-112">Supporta solo richieste `GET`.</span><span class="sxs-lookup"><span data-stu-id="12acd-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="12acd-113">Accetta espressioni di licenza o identificatori di eccezione di licenza come input nel modo specificato di seguito.</span><span class="sxs-lookup"><span data-stu-id="12acd-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="12acd-114">Si noti che tutti gli elementi delle espressioni di licenza fanno distinzione tra maiuscole e minuscole, pertanto tutti gli input a licenses.nuget.org faranno altrettanto distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="12acd-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="12acd-115">Espressioni di licenza</span><span class="sxs-lookup"><span data-stu-id="12acd-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="12acd-116">Richiesta</span><span class="sxs-lookup"><span data-stu-id="12acd-116">Request</span></span>

<span data-ttu-id="12acd-117">Le espressioni di licenza (inclusi i casi semplici in cui l'espressione è costituita da una singola licenza) devono essere [codificate in URL](https://tools.ietf.org/html/rfc3986#section-2.1) e usate come percorso nella richiesta a licenses.nuget.org.</span><span class="sxs-lookup"><span data-stu-id="12acd-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="12acd-118">Espressione di licenza</span><span class="sxs-lookup"><span data-stu-id="12acd-118">License expression</span></span> | <span data-ttu-id="12acd-119">URL da usare</span><span class="sxs-lookup"><span data-stu-id="12acd-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="12acd-120">MIT</span><span class="sxs-lookup"><span data-stu-id="12acd-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="12acd-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="12acd-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="12acd-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span><span class="sxs-lookup"><span data-stu-id="12acd-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="12acd-123">Il servizio supporta solo identificatori di licenza e identificatori di eccezione di licenza accettati da nuget.org. Tutte le espressioni di licenza che contengono identificatori di licenza o identificatori di eccezione di licenza non supportati o che non sono conformi alla sintassi delle espressioni di licenza vengono considerate non valide.</span><span class="sxs-lookup"><span data-stu-id="12acd-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="12acd-124">Risposta</span><span class="sxs-lookup"><span data-stu-id="12acd-124">Response</span></span>

<span data-ttu-id="12acd-125">Licenses.nuget.org risponde alle richieste contenenti espressioni di licenza valide con un codice di stato HTTP 200 e una pagina Web che contiene una descrizione dell'espressione di licenza:</span><span class="sxs-lookup"><span data-stu-id="12acd-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="12acd-126">Se l'espressione di licenza specificata contiene un unico identificatore di licenza, viene restituita una pagina Web contenente il testo di rifermento a tale licenza;</span><span class="sxs-lookup"><span data-stu-id="12acd-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="12acd-127">Se l'espressione di licenza specificata contiene un'espressione di licenza composita, viene restituita una pagina Web contenente l'espressione di licenza con i collegamenti alla singola licenza o ai riferimenti di eccezione di licenza.</span><span class="sxs-lookup"><span data-stu-id="12acd-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="12acd-128">Tutte le richieste contenenti un'espressione di licenza non valida generano una risposta HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="12acd-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="12acd-129">Eccezioni di licenza</span><span class="sxs-lookup"><span data-stu-id="12acd-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="12acd-130">Richiesta</span><span class="sxs-lookup"><span data-stu-id="12acd-130">Request</span></span>

<span data-ttu-id="12acd-131">Gli identificatori di eccezione di licenza devono essere codificati in URL e usati come percorso nella richiesta a licenses.nuget.org. In un'unica richiesta è possibile specificare uno solo identificatore di eccezione di licenza.</span><span class="sxs-lookup"><span data-stu-id="12acd-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="12acd-132">Nessun carattere aggiuntivo oltre all'identificatore di eccezione di licenza può essere incluso nella parte di percorso dell'URL.</span><span class="sxs-lookup"><span data-stu-id="12acd-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="12acd-133">Identificatore di eccezione di licenza</span><span class="sxs-lookup"><span data-stu-id="12acd-133">License exception identifier</span></span> | <span data-ttu-id="12acd-134">URL da usare</span><span class="sxs-lookup"><span data-stu-id="12acd-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="12acd-135">FLTK-exception</span><span class="sxs-lookup"><span data-stu-id="12acd-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="12acd-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="12acd-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="12acd-137">Risposta</span><span class="sxs-lookup"><span data-stu-id="12acd-137">Response</span></span>

<span data-ttu-id="12acd-138">Licenses.nuget.org risponde a una richiesta contenente un identificatore di eccezione di licenza noto con una risposta HTTP 200 e una pagina Web che contiene il testo di riferimento per l'eccezione di licenza specificata.</span><span class="sxs-lookup"><span data-stu-id="12acd-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="12acd-139">Tutte le richieste contenenti un identificatore di eccezione di licenza non supportato generano una risposta HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="12acd-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>