---
title: Note sulla versione 5.1 RTM di NuGet
description: Note sulla versione per NuGet 5.1 incluse nuove funzionalità, correzioni di bug e dcr.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 384145947b19af6577dc1255985df1a361c72bb5
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842571"
---
# <a name="nuget-51-release-notes"></a>Note sulla versione 5.1 di NuGet

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio| Disponibile in .NET SDK|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16.1](https://visualstudio.microsoft.com/downloads/) | [2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>installata con Visual Studio 2019 con carico di lavoro di .NET Core 

<sup>2</sup>disponibile in un'installazione facoltativa con Visual Studio 2019 con carico di lavoro di .NET Core

## <a name="summary-whats-new-in-51"></a>Riepilogo: Quali sono le novità nella versione 5.1

* Supporto per ignorare un push del pacchetto se esiste già per consentire una migliore integrazione con flussi di lavoro di integrazione continua/recapito Continuo - [1630 #](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Visual Studio offre ora un comodo collegamento per la pagina di gallery del pacchetto nuget.org - [5299 #](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* Il supporto per nuovi asset di .NET Core 3.0 come [Targeting Pack](https://github.com/dotnet/cli/issues/10006) e [pacchetti di Runtime](https://github.com/dotnet/cli/issues/10007)
  * NuGet pack e restore di supporto per FrameworkReferences abilitare i riferimenti ai pacchetti di runtime e di destinazione - [7342 #](https://github.com/NuGet/Home/issues/7342)
  * Scenario del pacchetto "solo download" di supporto con PackageDownload - [7339 #](https://github.com/NuGet/Home/issues/7339)
  * Runtime Exlcude e targeting Pack da risultati della ricerca e ripristino del grafico utilizzando PackageType - [7337 #](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

**Bug**

* Plug-in: i dettagli dell'eccezione persi durante la creazione del plug-in - [8057 #](https://github.com/NuGet/Home/issues/8057)

* Intervallo di PackageReference con limite inferiore a esclusivo non funziona se il limite inferiore è presente in una delle origini. - [#8054](https://github.com/NuGet/Home/issues/8054)

* Migliorare IsPackableFalseError messaggio - [8021 #](https://github.com/NuGet/Home/issues/8021)

* I pacchetti di File di blocco - file di blocco rigenerare quando viene modificato grafico progetto - [8019 #](https://github.com/NuGet/Home/issues/8019)

* Bug Project System: Rimuovere i pacchetti NuGet recupero automatico - [8017 #](https://github.com/NuGet/Home/issues/8017)

* Aggiungere una destinazione per la restituzione di FrameworkReference simile a CollectPackageDownloads e CollectPackageReferences - [8005 #](https://github.com/NuGet/Home/issues/8005)

* Cache HTTP:  Risorsa RepositoryResources non viene memorizzato nella cache in modo con controllo delle versioni - [7997 #](https://github.com/NuGet/Home/issues/7997)

* La registrazione: eccezione gli stack di chiamate non vengono segnalati con livello di dettaglio massimo - [7955 #](https://github.com/NuGet/Home/issues/7955)

* Modificare tutti gli URL di documentazione di NuGet per usare HTTPS - [7950 #](https://github.com/NuGet/Home/issues/7950)

* Migliorare il messaggio di avviso NU3024 - [7933 #](https://github.com/NuGet/Home/issues/7933)

* file di blocco non vengono aggiornati quando packagereference rimosso - [7930 #](https://github.com/NuGet/Home/issues/7930)

* Migliorare la gestione di casi di errore durante la convalida di un elemento licenseurl e licenza in nuspec - [7915 #](https://github.com/NuGet/Home/issues/7915)

* UI PM - fare clic sull'intestazione della scheda e facendo clic su "Apri percorso file" risultati errore - [7913 #](https://github.com/NuGet/Home/issues/7913)

* Plug-in: accedere al termine del processo di plug-in - [7907 #](https://github.com/NuGet/Home/issues/7907)

* Plug-in: frequenza dei conflitti elevata nei valori di data/ora di registrazione - [7899 #](https://github.com/NuGet/Home/issues/7899)

* Manifest.ReadFrom non riesce in qualsiasi file nuspec con LicenseExpression - [7894 #](https://github.com/NuGet/Home/issues/7894)

* RestoreLockedMode: NU1004 imprevisto quando ProjectReference fa riferimento a un progetto con personalizzato AssemblyName - [7889 #](https://github.com/NuGet/Home/issues/7889)

* Messaggio di errore migliore quando si verifica un errore di avvio del plug-in con un'eccezione - [7857 #](https://github.com/NuGet/Home/issues/7857)

* Quando si esegue un ripristino NoOp, evitare *. dgspec.json scrittura nella directory obj - [7854 #](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty = true non riesce a generare proprietà sulla mancata corrispondenza maiuscole - [7843 #](https://github.com/NuGet/Home/issues/7843)

* Impostazioni: carattere non valido nel percorso di origine può arrestarsi in modo anomalo Visual Studio - [7820 #](https://github.com/NuGet/Home/issues/7820)

* Se si elimina il file di blocco, restore non genera file di blocco su NoOp - [7807 #](https://github.com/NuGet/Home/issues/7807)

* URL della licenza e le cause di licenza con i metadati - errore di lettura [7547 #](https://github.com/NuGet/Home/issues/7547)

* Eccezioni non gestite nel V2FeedParser - [7523 #](https://github.com/NuGet/Home/issues/7523)

* NuGet.exe restituisce il codice di uscita zero per argomenti non validi - [7178 #](https://github.com/NuGet/Home/issues/7178)

* Aggiornare gli errori e alla documentazione di avviso in modo da riflettere scenari correlati firma - [6498 #](https://github.com/NuGet/Home/issues/6498)

* File di asset debba usare percorsi relativi per attivare lo spostamento dei progetti più facilmente - [4582 #](https://github.com/NuGet/Home/issues/4582)

**DCRs**

* Plug-in: abilitare la registrazione diagnostica - [7859 #](https://github.com/NuGet/Home/issues/7859)

* Marca 6 Tizen mappa alla versione 2.1 NetStandard - [7773 #](https://github.com/NuGet/Home/issues/7773)

**[Elenco di tutti i problemi risolti in questa versione: 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
