---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 4a40cc1f7d333e8d35a721f3eed2e6b9365faf7b
ms.sourcegitcommit: 8793f528a11bd8e8fb229cd12e9abba50d61e104
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/04/2019
ms.locfileid: "58921559"
---
# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>Spiegazione logica:

Con l'introduzione del [espressioni di licenza](nuspec.md#license), un requisito emersi affinché un servizio Reliable Services che fornirebbe un testo di riferimento per gli identificatori di singole licenze, gli identificatori di eccezioni o le espressioni di licenza.
Un ulteriore requisito per questo servizio è uno schema URL stabile, che non sia soggetta a collegare rot, in modo che è possibile usarlo in modo sicuro per garantire la compatibilità per i client meno recenti.

Licenses.NuGet.org soddisfa tale ruolo. NuGet.org lo usa per fornire il riferimento al testo di licenza per i pacchetti che specificano la licenza di utilizzo di un'espressione di licenza. `nuget pack` o compressione con altre [gli strumenti client](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) impostare il [ `licenseUrl` ](nuspec.md#licenseurl) elemento in modo che punti a licenses.nuget.org per garantire la compatibilità con client meno recenti che non supportano il `license` elemento.

## <a name="protocol"></a>Protocollo

Nessuna risposta leggibile dal computer Licenses.NuGet.org è destinato a essere visualizzati dagli utenti nei propri browser, è disponibili.
Deve essere usato il protocollo HTTPS e le richieste dovrebbero essere creata in un determinato modo. Supporta solo `GET` richieste.
Accetta le espressioni di licenza o gli identificatori di eccezioni di licenza come input in modo specificato di seguito. Si noti che tutti gli elementi delle espressioni di licenza sono tra maiuscole e minuscole, e pertanto tutti gli input per licenses.nuget.org distinzione maiuscole / minuscole anche.

### <a name="license-expressions"></a>Espressioni di licenza

#### <a name="request"></a>Richiesta

Le espressioni di licenza (inclusi i casi semplici quando l'espressione è costituita da una singola licenza) devono essere [codificata in URL](https://tools.ietf.org/html/rfc3986#section-2.1) e usato come un percorso nella richiesta alla licenses.nuget.org.

| Espressione di licenza | URL da usare |
|:---|:---|
| MIT                                                | <https://licenses.nuget.org/MIT> |
| (MIT)                                              | <https://licenses.nuget.org/(MIT)> |
| (LGPL-2.0-only con Apache OR FLTK eccezione-2.0+) | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

Il servizio supporta solo identificatori di licenza e gli identificatori di eccezione licenza accettati da nuget.org. Tutte le espressioni di licenza che contengono gli identificatori di licenza non supportato o gli identificatori di eccezioni di licenza o che non è conforme alla sintassi delle espressioni di licenza vengono considerate non validi.

#### <a name="response"></a>Risposta

Licenses.NuGet.org risponde alle richieste contenenti espressioni di licenza valida con un codice di stato HTTP 200 e una pagina web contenente una descrizione dell'espressione di licenza:

* Se fornito espressione licenza contiene un identificatore di licenza per singolo che viene restituita una pagina web che contiene tale testo riferimento licenza;
* Se non fornito licenza espressione è un'espressione composta licenza, viene restituita una pagina web che contiene l'espressione di licenza con collegamenti alle singole licenze o riferimenti a eccezione di licenza.

Tutte le richieste che contengono un risultato dell'espressione licenza non valida in una risposta HTTP 404.

### <a name="license-exceptions"></a>Eccezioni di licenza

#### <a name="request"></a>Richiesta

Gli identificatori di eccezioni di licenza devono essere utilizzato come un percorso nella richiesta alla licenses.nuget.org e codificato con URL. È possibile fornire solo un identificatore di eccezione licenza singola in un'unica richiesta. Nessun carattere aggiuntivo oltre all'identificatore di eccezione licenza possono essere presenti nella parte di percorso dell'URL.

| Identificatore di eccezione di licenza | URL da usare |
|:---|:---|
|FLTK-eccezione            | <https://licenses.nuget.org/FLTK-exception> |
|openvpn-openssl-exception | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a>Risposta

Licenses.NuGet.org risponde a una richiesta con un identificatore di eccezione licenza note con una risposta HTTP 200 e una pagina web contenente il testo di riferimento per l'eccezione di licenza specificato.

Qualsiasi richiesta che contiene un identificatore di eccezione non supportata licenza comporta una risposta HTTP 404.