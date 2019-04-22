---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 4a40cc1f7d333e8d35a721f3eed2e6b9365faf7b
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "58921559"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="18a14-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="18a14-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="18a14-103">Spiegazione logica:</span><span class="sxs-lookup"><span data-stu-id="18a14-103">Rationale</span></span>

<span data-ttu-id="18a14-104">Con l'introduzione del [espressioni di licenza](nuspec.md#license), un requisito emersi affinché un servizio Reliable Services che fornirebbe un testo di riferimento per gli identificatori di singole licenze, gli identificatori di eccezioni o le espressioni di licenza.</span><span class="sxs-lookup"><span data-stu-id="18a14-104">With the introduction of the [license expressions](nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="18a14-105">Un ulteriore requisito per questo servizio è uno schema URL stabile, che non sia soggetta a collegare rot, in modo che è possibile usarlo in modo sicuro per garantire la compatibilità per i client meno recenti.</span><span class="sxs-lookup"><span data-stu-id="18a14-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="18a14-106">Licenses.NuGet.org soddisfa tale ruolo.</span><span class="sxs-lookup"><span data-stu-id="18a14-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="18a14-107">NuGet.org lo usa per fornire il riferimento al testo di licenza per i pacchetti che specificano la licenza di utilizzo di un'espressione di licenza.</span><span class="sxs-lookup"><span data-stu-id="18a14-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="18a14-108">`nuget pack` o compressione con altre [gli strumenti client](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) impostare il [ `licenseUrl` ](nuspec.md#licenseurl) elemento in modo che punti a licenses.nuget.org per garantire la compatibilità con client meno recenti che non supportano il `license` elemento.</span><span class="sxs-lookup"><span data-stu-id="18a14-108">`nuget pack` or packing with other [client tools](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) set the [`licenseUrl`](nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="18a14-109">Protocollo</span><span class="sxs-lookup"><span data-stu-id="18a14-109">Protocol</span></span>

<span data-ttu-id="18a14-110">Nessuna risposta leggibile dal computer Licenses.NuGet.org è destinato a essere visualizzati dagli utenti nei propri browser, è disponibili.</span><span class="sxs-lookup"><span data-stu-id="18a14-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="18a14-111">Deve essere usato il protocollo HTTPS e le richieste dovrebbero essere creata in un determinato modo.</span><span class="sxs-lookup"><span data-stu-id="18a14-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="18a14-112">Supporta solo `GET` richieste.</span><span class="sxs-lookup"><span data-stu-id="18a14-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="18a14-113">Accetta le espressioni di licenza o gli identificatori di eccezioni di licenza come input in modo specificato di seguito.</span><span class="sxs-lookup"><span data-stu-id="18a14-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="18a14-114">Si noti che tutti gli elementi delle espressioni di licenza sono tra maiuscole e minuscole, e pertanto tutti gli input per licenses.nuget.org distinzione maiuscole / minuscole anche.</span><span class="sxs-lookup"><span data-stu-id="18a14-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="18a14-115">Espressioni di licenza</span><span class="sxs-lookup"><span data-stu-id="18a14-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="18a14-116">Richiesta</span><span class="sxs-lookup"><span data-stu-id="18a14-116">Request</span></span>

<span data-ttu-id="18a14-117">Le espressioni di licenza (inclusi i casi semplici quando l'espressione è costituita da una singola licenza) devono essere [codificata in URL](https://tools.ietf.org/html/rfc3986#section-2.1) e usato come un percorso nella richiesta alla licenses.nuget.org.</span><span class="sxs-lookup"><span data-stu-id="18a14-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="18a14-118">Espressione di licenza</span><span class="sxs-lookup"><span data-stu-id="18a14-118">License expression</span></span> | <span data-ttu-id="18a14-119">URL da usare</span><span class="sxs-lookup"><span data-stu-id="18a14-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="18a14-120">MIT</span><span class="sxs-lookup"><span data-stu-id="18a14-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="18a14-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="18a14-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="18a14-122">(LGPL-2.0-only con Apache OR FLTK eccezione-2.0+)</span><span class="sxs-lookup"><span data-stu-id="18a14-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="18a14-123">Il servizio supporta solo identificatori di licenza e gli identificatori di eccezione licenza accettati da nuget.org. Tutte le espressioni di licenza che contengono gli identificatori di licenza non supportato o gli identificatori di eccezioni di licenza o che non è conforme alla sintassi delle espressioni di licenza vengono considerate non validi.</span><span class="sxs-lookup"><span data-stu-id="18a14-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="18a14-124">Risposta</span><span class="sxs-lookup"><span data-stu-id="18a14-124">Response</span></span>

<span data-ttu-id="18a14-125">Licenses.NuGet.org risponde alle richieste contenenti espressioni di licenza valida con un codice di stato HTTP 200 e una pagina web contenente una descrizione dell'espressione di licenza:</span><span class="sxs-lookup"><span data-stu-id="18a14-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="18a14-126">Se fornito espressione licenza contiene un identificatore di licenza per singolo che viene restituita una pagina web che contiene tale testo riferimento licenza;</span><span class="sxs-lookup"><span data-stu-id="18a14-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="18a14-127">Se non fornito licenza espressione è un'espressione composta licenza, viene restituita una pagina web che contiene l'espressione di licenza con collegamenti alle singole licenze o riferimenti a eccezione di licenza.</span><span class="sxs-lookup"><span data-stu-id="18a14-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="18a14-128">Tutte le richieste che contengono un risultato dell'espressione licenza non valida in una risposta HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="18a14-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="18a14-129">Eccezioni di licenza</span><span class="sxs-lookup"><span data-stu-id="18a14-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="18a14-130">Richiesta</span><span class="sxs-lookup"><span data-stu-id="18a14-130">Request</span></span>

<span data-ttu-id="18a14-131">Gli identificatori di eccezioni di licenza devono essere utilizzato come un percorso nella richiesta alla licenses.nuget.org e codificato con URL. È possibile fornire solo un identificatore di eccezione licenza singola in un'unica richiesta.</span><span class="sxs-lookup"><span data-stu-id="18a14-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="18a14-132">Nessun carattere aggiuntivo oltre all'identificatore di eccezione licenza possono essere presenti nella parte di percorso dell'URL.</span><span class="sxs-lookup"><span data-stu-id="18a14-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="18a14-133">Identificatore di eccezione di licenza</span><span class="sxs-lookup"><span data-stu-id="18a14-133">License exception identifier</span></span> | <span data-ttu-id="18a14-134">URL da usare</span><span class="sxs-lookup"><span data-stu-id="18a14-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="18a14-135">FLTK-eccezione</span><span class="sxs-lookup"><span data-stu-id="18a14-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="18a14-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="18a14-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="18a14-137">Risposta</span><span class="sxs-lookup"><span data-stu-id="18a14-137">Response</span></span>

<span data-ttu-id="18a14-138">Licenses.NuGet.org risponde a una richiesta con un identificatore di eccezione licenza note con una risposta HTTP 200 e una pagina web contenente il testo di riferimento per l'eccezione di licenza specificato.</span><span class="sxs-lookup"><span data-stu-id="18a14-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="18a14-139">Qualsiasi richiesta che contiene un identificatore di eccezione non supportata licenza comporta una risposta HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="18a14-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>