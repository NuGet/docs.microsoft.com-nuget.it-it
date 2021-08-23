---
title: Deprecazione dei pacchetti nuget.org
description: Descrizione dettagliata del processo di deprecazione dei pacchetti e del modo in cui i client visualizzano queste informazioni
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 4a6dbd645cb72b0085fd0347def58ade134fc5ee
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726964"
---
# <a name="deprecating-packages"></a>Deprecazione dei pacchetti

È possibile deprecazione di un pacchetto se non si gestisce più un pacchetto o se si desidera incoraggiare i consumer del pacchetto a passare a un altro pacchetto. 

La deprecazione del pacchetto è diversa **dall'annullamento dell'elenco,** come illustrato di seguito:
* **L'annullamento dell'elenco** di un pacchetto ne impedisce l'individuazione perché è nascosto nei risultati della ricerca. 
* **La** deprecazione di un pacchetto consente ai consumer esistenti del pacchetto di scoprire se è installato o usato nei progetti. Consente inoltre di conoscere il motivo della deprecazione e un pacchetto consigliato alternativo, come specificato dall'autore del pacchetto. La deprecazione di un pacchetto non annulla l'elenco del pacchetto. 

In quanto editore, è possibile scegliere sia di rimuovere dall'elenco sia di deprecazione dei pacchetti.

## <a name="deprecation-workflow"></a>Flusso di lavoro di deprecazione
1. Per deprecazione di un pacchetto, passare **a Gestisci pacchetti** e selezionare **Deprecazione:**

    ![Opzione Vai a deprecazione pacchetto](media/deprecation-select-option.png)

2. Selezionare la versione che si vuole deprecare. Se si vuole deprecare tutte le versioni, scegliere **l'opzione Seleziona tutte le** versioni.

    ![Selezionare le versioni del pacchetto da deprecare](media/deprecation-select-version.png)

3. Scegliere un motivo per la deprecazione. Se il pacchetto non viene più gestito, scegliere **l'opzione Legacy.** Se la versione specifica presenta un bug critico, scegliere **l'opzione con bug** critici. Per qualsiasi altro motivo, selezionare **Altro**. È sempre possibile specificare un pacchetto consigliato alternativo (e la versione) e un messaggio personalizzato per i proprietari. 

    ![Selezionare i motivi per cui consigliare un pacchetto alternativo e un messaggio personalizzato](media/deprecation-save.png)

> [!Note]
> Il messaggio personalizzato viene visualizzato solo nuget.org ma non dai client. Attualmente, i client come `dotnet.exe` e NuGet Gestione pacchetti non visualizzano il messaggio personalizzato.

## <a name="client-experience-for-deprecated-packages"></a>Esperienza client per i pacchetti deprecati
Dopo che un pacchetto è stato deprecato, i consumer ne vengono informati nei modi seguenti (a seconda del client usato).

### <a name="visual-studio"></a>Visual Studio 
*Disponibile a partire Visual Studio 2019 versione 16.3*

Visual Studio avvisa dell'utilizzo di un pacchetto deprecato nella `Installed` scheda. Verrà visualizzato un avviso per il pacchetto e le relative informazioni sulla deprecazione( incluso il motivo per cui è stato deprecato e il pacchetto alternativo da usare, se presente).

   ![Pacchetti deprecati nella Visual Studio installata di Gestione pacchetti](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*Disponibile a partire da .NET SDK 3.0*

Se si usa dotnet.exe, è possibile eseguire il comando nella cartella della soluzione o del progetto per ottenere un elenco di pacchetti deprecati insieme alle informazioni `dotnet list package --deprecated` sulla deprecazione:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```

## <a name="transfer-popularity-to-a-newer-package"></a>Trasferire popolarità a un pacchetto più recente

Gli autori di pacchetti che hanno deprecato un pacchetto legacy possono scegliere di trasferire la "popolarità" a un pacchetto più recente per migliorare la classificazione di ricerca del pacchetto più recente. Ciò consente ai clienti di individuare il pacchetto più recente anziché il pacchetto deprecato.

Si supponga, ad esempio, di avere due pacchetti:

* Pacchetto legacy deprecato, `Contoso.Legacy` con 3 milioni di download
* Pacchetto più recente, `Contoso.Latest` con 5 download

NuGet.org preferisce i risultati della ricerca con download/popolarità più elevati. Data la query di ricerca "Contoso", è probabile che il pacchetto deprecato sia al di `Contoso.Legacy` sopra del pacchetto più recente nei risultati della `Contoso.Latest` ricerca.

Per risolvere questo problema, è possibile richiedere il trasferimento della popolarità del pacchetto legacy deprecato al pacchetto più recente. In questo modo la classificazione nei risultati della ricerca è più elevata, mentre la classificazione `Contoso.Latest` `Contoso.Legacy` è inferiore. Sono interessati solo i punteggi di popolarità interni per i pacchetti, ma il conteggio effettivo dei download per ogni pacchetto non verrà influenzato.

> [!Note]
> I trasferimenti di popolarità possono rendere molto più difficile per i consumer trovare il pacchetto legacy.

Vedere la tabella seguente per avere un'idea concreta dell'impatto di un trasferimento di popolarità sulle classificazioni di ricerca per la query "Contoso":

| Classificazione della ricerca    | Prima del trasferimento della popolarità        | Dopo il trasferimento della popolarità         |
|----------------   |--------------------------------   |--------------------------------   |
| 1                 | *Contoso.Legacy, download 3M*    | *Contoso.Latest, 5 download*     |
| 2                 | Contoso.Scanner, download da 2 milioni     | Contoso.Scanner, download da 2 milioni     |
| 3                 | Contoso.Core, download da 1,5 milioni     | Contoso.Core, download da 1,5 milioni     |
| 4                 | Contoso.UI, download da 1 m          | Contoso.UI, download da 1 m          |
| ...               | ...                               | ...                               |
| 20                | *Contoso.Latest, 5 download*     | *Contoso.Legacy, download 3M*    |

### <a name="popularity-transfer-application-process"></a>Processo di applicazione di trasferimento della popolarità

1. Esaminare i requisiti [di trasferimento della popolarità](#popularity-transfer-requirements).
2. Inviare un messaggio di posta elettronica con il pacchetto deprecato di cui deve essere trasferita la popolarità e l'elenco dei pacchetti stabili che devono ricevere [account@nuget.org](mailto:account@nuget.org) il trasferimento di popolarità.

Dopo l'invio dell'applicazione, verrà inviata una notifica dell'accettazione o del rifiuto dell'applicazione (con i criteri che hanno causato il rifiuto). Potrebbe essere necessario porre altre domande di identificazione per verificare l'identità del proprietario.

#### <a name="popularity-transfer-requirements"></a>Requisiti di trasferimento della popolarità

* I pacchetti legacy e i nuovi pacchetti devono condividere tutti i proprietari.
* I nuovi pacchetti devono essere chiaramente correlati ai pacchetti legacy per la denominazione e la funzione, ad esempio un'evoluzione o una generazione successiva.
* Tutte le versioni dei pacchetti legacy devono essere deprecate e puntare ai nuovi pacchetti che ricevono il trasferimento.
* Il trasferimento della popolarità non deve causare confusione per NuGet utenti o peggiorare l'esperienza NuGet ricerca.
* I nuovi pacchetti devono avere una versione stabile.
* Il pacchetto legacy non deve ricevere trasferimenti di popolarità da un altro pacchetto deprecato.

### <a name="advanced-popularity-transfer-scenarios"></a>Scenari avanzati di trasferimento di popolarità

#### <a name="package-consolidations"></a>Consolidamenti dei pacchetti

È possibile trasferire la popolarità di più pacchetti deprecati a favore di un singolo nuovo pacchetto. Si supponga, ad esempio, di avere 3 pacchetti:

* Il primo pacchetto legacy deprecato, `Contoso.Legacy1`
* Il secondo pacchetto legacy deprecato, `Contoso.Legacy2`
* Il nuovo pacchetto consolidato, `Contoso.Latest`

Dopo aver deprecato `Contoso.Legacy1` e , è possibile applicare per trasferire la loro popolarità a `Contoso.Legacy2` `Contoso.Latest` .

#### <a name="package-splits"></a>Suddivisioni dei pacchetti

La popolarità di un pacchetto deprecato può essere trasferita e divisa tra un massimo di 5 pacchetti più nuovi. Ciò è utile se la funzionalità di un pacchetto deprecato è stata suddivisa tra più nuovi pacchetti. Si supponga, ad esempio, di avere 3 pacchetti:

* Pacchetto legacy deprecato `Contoso.Legacy`
* Il primo nuovo pacchetto, `Contoso.Web`
* Il secondo nuovo pacchetto, `Contoso.Cloud`

`Contoso.Legacy` include funzionalità Web e cloud, ma ho deciso di separare tale funzionalità in pacchetti diversi per la prossima generazione. Dopo la `Contoso.Legacy` deprecazione di , è possibile applicare per trasferire la popolarità sia a che a `Contoso.Web` `Contoso.Cloud` .

> [!Warning]
> La popolarità trasferita verrà suddivisa in modo uniforme tra tutti i nuovi pacchetti. Di conseguenza, è consigliabile trasferire la popolarità del pacchetto deprecato al numero più contenuto possibile di pacchetti.

#### <a name="popularity-transfer-chains"></a>Catene di trasferimento di popolarità

Un pacchetto deprecato non può trasferire la popolarità se sta già ricevendo popolarità da un altro pacchetto deprecato. Ad esempio, si supponga di avere 3 pacchetti:

* Pacchetto legacy deprecato `Contoso.First`
* Pacchetto legacy deprecato `Contoso.Second`
* Il nuovo pacchetto, `Contoso.Latest`

Se `Contoso.First` trasferisce la sua popolarità a `Contoso.Second,` , non può trasferire la sua popolarità a `Contoso.Second` `Contoso.Latest` . È invece consigliabile trasferire la popolarità di e `Contoso.First` a , in base allo scenario di `Contoso.Second` `Contoso.Latest` [consolidamento dei](#package-consolidations) pacchetti.
