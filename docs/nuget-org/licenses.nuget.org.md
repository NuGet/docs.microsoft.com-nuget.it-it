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
# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>Spiegazione logica:

Con l'introduzione delle [espressioni di licenza](../reference/nuspec.md#license), è nata l'esigenza di avere un servizio affidabile che specificasse un testo di riferimento per ogni identificatore di licenza, identificatore di eccezione o espressione di licenza.
Un requisito aggiuntivo per questo servizio è la necessità di uno schema URL stabile, che non sia soggetto alla rottura dei collegamenti, ma che possa invece essere usato in modo sicuro per assicurare ai client meno recenti compatibilità con le versioni precedenti.

Licenses.NuGet.org è il servizio adatto. Viene usato da Nuget.org per creare il riferimento di testo della licenza per i pacchetti che specificano la licenza usando un'espressione di licenza. Con il comando `nuget pack` o la compressione di altri [strumenti client](../install-nuget-client-tools.md) si imposta l'elemento [`licenseUrl`](../reference/nuspec.md#licenseurl) in modo che faccia riferimento a licenses.nuget.org to per assicurare compatibilità con le versioni precedenti ai client meno recenti che non supportano l'elemento `license`.

## <a name="protocol"></a>Protocollo

Licenses.nuget.org è destinato a essere visualizzato dagli utenti nei browser. Non sono previste risposte leggibili al computer.
È necessario usare il protocollo HTTPS e le richieste devono essere costruite in un modo specifico. Supporta solo richieste `GET`.
Accetta espressioni di licenza o identificatori di eccezione di licenza come input nel modo specificato di seguito. Si noti che tutti gli elementi delle espressioni di licenza fanno distinzione tra maiuscole e minuscole, pertanto tutti gli input a licenses.nuget.org faranno altrettanto distinzione tra maiuscole e minuscole.

### <a name="license-expressions"></a>Espressioni di licenza

#### <a name="request"></a>Richiesta

Le espressioni di licenza (inclusi i casi semplici in cui l'espressione è costituita da una singola licenza) devono essere [codificate in URL](https://tools.ietf.org/html/rfc3986#section-2.1) e usate come percorso nella richiesta a licenses.nuget.org.

| Espressione di licenza | URL da usare |
|:---|:---|
| MIT                                                | <https://licenses.nuget.org/MIT> |
| (MIT)                                              | <https://licenses.nuget.org/(MIT)> |
| (LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+) | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

Il servizio supporta solo identificatori di licenza e identificatori di eccezione di licenza accettati da nuget.org. Tutte le espressioni di licenza che contengono identificatori di licenza o identificatori di eccezione di licenza non supportati o che non sono conformi alla sintassi delle espressioni di licenza vengono considerate non valide.

#### <a name="response"></a>Risposta

Licenses.nuget.org risponde alle richieste contenenti espressioni di licenza valide con un codice di stato HTTP 200 e una pagina Web che contiene una descrizione dell'espressione di licenza:

* Se l'espressione di licenza specificata contiene un unico identificatore di licenza, viene restituita una pagina Web contenente il testo di rifermento a tale licenza;
* Se l'espressione di licenza specificata contiene un'espressione di licenza composita, viene restituita una pagina Web contenente l'espressione di licenza con i collegamenti alla singola licenza o ai riferimenti di eccezione di licenza.

Tutte le richieste contenenti un'espressione di licenza non valida generano una risposta HTTP 404.

### <a name="license-exceptions"></a>Eccezioni di licenza

#### <a name="request"></a>Richiesta

Gli identificatori di eccezione di licenza devono essere codificati in URL e usati come percorso nella richiesta a licenses.nuget.org. In un'unica richiesta è possibile specificare uno solo identificatore di eccezione di licenza. Nessun carattere aggiuntivo oltre all'identificatore di eccezione di licenza può essere incluso nella parte di percorso dell'URL.

| Identificatore di eccezione di licenza | URL da usare |
|:---|:---|
|FLTK-exception            | <https://licenses.nuget.org/FLTK-exception> |
|openvpn-openssl-exception | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a>Risposta

Licenses.nuget.org risponde a una richiesta contenente un identificatore di eccezione di licenza noto con una risposta HTTP 200 e una pagina Web che contiene il testo di riferimento per l'eccezione di licenza specificata.

Tutte le richieste contenenti un identificatore di eccezione di licenza non supportato generano una risposta HTTP 404.