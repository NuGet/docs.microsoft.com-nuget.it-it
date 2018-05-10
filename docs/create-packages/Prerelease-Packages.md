---
title: Versioni non definitive nei pacchetti NuGet
description: Linee guida per la compilazione di versioni non definitive dei pacchetti
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: a4540d29d9ca01f98ee5d1786e8a175ee0ea79f4
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="building-pre-release-packages"></a>Compilazione di versioni non definitive dei pacchetti

Ogni volta che si rilascia un pacchetto aggiornato con un nuovo numero di versione, NuGet considera tale versione l'ultima versione stabile, come illustrato, ad esempio, nell'interfaccia utente di Gestione pacchetti all'interno di Visual Studio:

![Interfaccia utente di Gestione pacchetti che mostra l'ultima versione stabile](media/Prerelease_01-LatestStable.png)

Una versione stabile è una versione considerata sufficientemente affidabile da poter essere usata in ambiente di produzione. L'ultima versione stabile è anche quella che verrà installata come aggiornamento del pacchetto oppure durante il ripristino del pacchetto (soggetto a vincoli, come descritto in [Reinstallazione e aggiornamento di pacchetti](../consume-packages/reinstalling-and-updating-packages.md)).

Per supportare il ciclo di vita di rilascio del software, NuGet 1.6 e versioni successive consentono la distribuzione di pacchetti in versione non definitiva, in cui il numero di versione include un suffisso per il controllo delle versioni semantico, ad esempio `-alpha`, `-beta` o `-rc`. Per altre informazioni, vedere [Controllo delle versioni dei pacchetti](../reference/package-versioning.md#pre-release-versions).

È possibile specificare tali versioni in due modi:

- File `.nuspec`: includere il suffisso di versione semantico nell'elemento `version`:

    ```xml
    <version>1.0.1-alpha</version>
    ```

- Attributi dell'assembly: quando si compila un pacchetto da un progetto di Visual Studio (`.csproj` o `.vbproj`), usare `AssemblyInformationalVersionAttribute` per specificare la versione:

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    NuGet preleva questo valore anziché quello specificato nell'attributo `AssemblyVersion`, che non supporta il versionamento semantico.

Quando si è pronti per rilasciare una versione stabile, è sufficiente rimuovere il suffisso e il pacchetto ottiene la precedenza rispetto a qualsiasi altra versione non definitiva. Vedere di nuovo [Controllo delle versioni dei pacchetti](../reference/package-versioning.md#pre-release-versions).

## <a name="installing-and-updating-pre-release-packages"></a>Installazione e aggiornamento di pacchetti in versione non definitiva

Per impostazione predefinita, NuGet non include le versioni non definitive quando si lavora con i pacchetti, ma è possibile modificare questo comportamento come segue:

- **Interfaccia utente di Gestione pacchetti in Visual Studio**: nell'interfaccia utente di **Gestisci pacchetti NuGet** selezionare la casella di controllo **Includi versione preliminare**:

    ![Casella di controllo Includi versione preliminare in Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    La selezione o la deselezione di questa casella di controllo aggiorna l'interfaccia utente di Gestione pacchetti e l'elenco delle versioni disponibili che è possibile installare.

- **Console di Gestione pacchetti**: usare l'opzione `-IncludePrerelease` con i comandi `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` e `Update-Package`. Vedere [Informazioni di riferimento su PowerShell](../tools/powershell-reference.md).

- **Interfaccia della riga di comando di NuGet**: usare l'opzione `-prerelease` con i comandi `install`, `update`, `delete` e `mirror`. Vedere [NuGet CLI reference](../tools/nuget-exe-cli-reference.md) (Informazioni di riferimento sull'interfaccia della riga di comando di NuGet).

## <a name="semantic-versioning"></a>Versionamento semantico

La [convenzione di versionamento semantico o SemVer](http://semver.org/spec/v1.0.0.html) descrive come usare le stringhe nei numeri di versione per indicare il significato del codice sottostante.

In questa convenzione, ogni versione è composta di tre parti, `Major.Minor.Patch`, con il significato seguente:

- `Major`: modifiche importanti
- `Minor`: nuove funzionalità, ma compatibili con le versioni precedenti
- `Patch`: solo correzioni di bug compatibili con le versioni precedenti

Le versioni non definitive vengono quindi contrassegnate aggiungendo un trattino e una stringa dopo il numero di patch. Tecnicamente, è possibile usare *qualsiasi* stringa dopo il trattino e NuGet considererà il pacchetto come in versione non definitiva. NuGet visualizza quindi il numero di versione completo nell'interfaccia utente applicabile, lasciando ai consumer l'interpretazione del significato.

Tenendo conto di questo aspetto, è in genere consigliabile seguire convenzioni di denominazione riconosciute, come le seguenti:

- `-alpha`: versione alfa, usata in genere per lavori in corso e sperimentazione
- `-beta`: versione beta, in genere completa dal punto di vista funzionale per il successivo rilascio pianificato, ma può contenere bug noti.
- `-rc`: versione finale candidata, in genere potenzialmente finale (stabile) se non emergono bug significativi.

> [!Note]
> NuGet 4.3.0+ supporta il [versionamento semantico v2.0.0](http://semver.org/spec/v2.0.0.html), ovvero numeri di versione non definitiva con la notazione con punto, come in `1.0.1-build.23`. La notazione con punto non è supportata con le versioni di NuGet precedenti alla versione 4.3.0. Nelle versioni precedenti di NuGet è possibile usare un formato come `1.0.1-build23`, ma viene sempre considerato una versione non definitiva.

Indipendentemente dai suffissi usati, tuttavia, NuGet stabilirà sempre la precedenza in ordine alfabetico inverso:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

Come illustrato, la versione senza suffisso avrà sempre la precedenza rispetto alle versioni non definitive. Si noti inoltre che se si usano suffissi numerici con i tag di versione non definitiva che potrebbero usare numeri a due cifre (o più), è buona norma usare zeri iniziali come in beta01 e beta05 per assicurare un ordinamento corretto con l'aumentare dei numeri.
