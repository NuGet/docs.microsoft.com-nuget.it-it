---
title: Ripristino NuGet errori e avvisi riferimento | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: b76b8a00-7155-4163-b533-894086d2ef78
description: Riferimento complete per avvisi ed errori generati da NuGet durante il ripristino del pacchetto
keywords: NuGet errori, avvisi NuGet, diagnostica
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 53fccbb86f2920d870b5383070d043e25045a626
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="errors-and-warnings"></a>Errori e avvisi

In NuGet 4.3.0, errori e avvisi sono numerati come descritto in questo argomento e forniscono informazioni dettagliate che consentono di risolvere i problemi che interessano. 

Gli errori e avvisi elencati di seguito sono disponibili solo con [basato su PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) progetti e NuGet 4.3.0. NuGet anche rispetta la proprietà di MSBuild per l'esclusione di avvisi o li elevare a errori. Per ulteriori informazioni, vedere [procedura: esclusione di avvisi del compilatore](/visualstudio/ide/how-to-suppress-compiler-warnings) nella documentazione di Visual Studio.

**Errori**

| Gruppo | Numeri di errore |
| --- | --- |
| [Errori di input non validi](#invalid-input-errors) | [NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003) |
| [Errori di pacchetto e progetto mancanti](#missing-package-and-project-errors) | [NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [ NU1106](#nu1106), [NU1107](#nu1107) (in precedenza NU1607), [NU1108](#nu1107) (in precedenza NU1606) |
| [Errori di compatibilità](#compatibility-errors) | [NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401) |

**Avvisi**

| Gruppo | Numeri di avviso |
| --- | --- |
| [Avvisi di input non validi](#invalid-input-warnings) | [NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503) |
| [Avvisi di versione di pacchetto imprevisto](#unexpected-package-version-warnings) | [NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605) |
| [Avvisi di sistema di risoluzione dei conflitti](#resolver-conflict-warnings) | [NU1608](#nu1608) |
| [Avvisi di fallback di pacchetto](#package-fallback-warnings) | [NU1701](#nu1701) |
| [Feed di avvisi](#feed-warnings) | [NU1801](#nu1801) |
| [Avvisi ed errori interni di NuGet](#nuget-internal-errors-and-warnings) | [NU1000](#nu1000), [NU1500](#nu1500) |

## <a name="invalid-input-errors"></a>Errori di input non validi

[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)

### <a name="nu1001"></a>NU1001

| | |
| --- | --- |
| **Problema** | Il progetto non contiene uno o più Framework. |
| **Cause più comuni** | Il progetto non contiene un `TargetFramework` o `TargetFrameworks` proprietà. |
| **Messaggio di esempio** | *ProjA il progetto non specifica alcun framework di destinazione in c:\tmp\projA.csproj* |

### <a name="nu1002"></a>NU1002

| | |
| --- | --- |
| **Problema** | Combinazione non valida di input con una parola chiave non CRITTOGRAFATO. |
| **Cause più comuni** | CLEAR non possono essere combinati con altri input. |
| **Messaggio di esempio** | *'CLEAR' non può essere utilizzato in combinazione con altri valori* |

### <a name="nu1003"></a>NU1003

| | |
| --- | --- |
| **Problema** | `PackageTargetFallback`e `AssetTargetFallback` comportamenti diversi per la selezione di risorse e non possono essere utilizzati insieme. |
| **Cause più comuni** | Entrambi `PackageTargetFallback` e `AssetTargetFallback` esiste nel progetto. |
| **Messaggio di esempio** | *PackageTargetFallback e AssetTargetFallback non possono essere utilizzati insieme. Rimuovere i riferimenti di PackageTargetFallback(deprecated) dall'ambiente del progetto.* |

## <a name="missing-package-and-project-errors"></a>Errori di pacchetto e progetto mancanti

[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104 ](#nu1104)  |  [NU1105](#nu1105) | [NU1106](#nu1106)

### <a name="nu1100"></a>NU1100

| | |
| --- | --- |
| **Problema** | Un gruppo di dipendenze non essere risolto. Questo è un problema generico per tipi che non sono pacchetti o progetti. |
| **Cause più comuni** | Il progetto contiene una dipendenza su un elemento che non esiste. |
| **Messaggio di esempio** | *Impossibile risolvere System.Missing per net45* |

### <a name="nu1101"></a>NU1101

| | |
| --- | --- |
| **Problema** | Impossibile trovare il pacchetto su tutte le origini. |
| **Cause più comuni** | L'origine del pacchetto corretto è manca o l'identificatore del pacchetto non è corretto. |
| **Messaggio di esempio** | *Impossibile trovare il pacchetto System.Missing. Nessun pacchetto esistenti con questo id nelle origini: dotnet-core, dotnet roslyn, nuget.org* |

### <a name="nu1102"></a>NU1102

| | |
| --- | --- |
| **Problema** | L'identificatore del pacchetto è stato trovato ma presente una versione all'interno dell'intervallo di dipendenza specificata non può essere una delle origini. |
| **Cause più comuni** | L'origine del pacchetto corretto è manca o l'intervallo di dipendenza non è corretto. L'intervallo può essere specificato da un pacchetto e non dell'utente. L'utente potrebbe essere necessario passare a una versione disponibile se il pacchetto fa riferimento direttamente il progetto. |
| **Messaggio di esempio** | *Impossibile trovare il pacchetto NuGet.Versioning con la versione (> = 9.0.1)<br/> -30 trovare versioni in nuget.org [più vicino di versione: 4.0.0]<br/> -versioni 10 trovato in dotnet buildtools [più vicino di versione: 4.0.0-rc-2129]<br/> -9 trovato versioni in NuGetVolatile [più vicino di versione: 3.0.0-beta-00032]<br/> -0 versioni, vedere dotnet core<br/> -0 versioni, vedere dotnet roslyn* |

### <a name="nu1103"></a>NU1103

| | |
| --- | --- |
| **Problema** | Nessuna versione stabile sono stata trovata nell'intervallo di dipendenza. Le versioni non definitive sono state trovate, ma non sono consentite. |
| **Cause più comuni** | Il progetto specificato una versione stabile per l'intervallo di dipendenza. Gli utenti devono modificare l'intervallo di versione per includere le versioni non definitive. |
| **Messaggio di esempio** | *Impossibile trovare un pacchetto stabile NuGet.Versioning con la versione (> = 3.0.0)<br/> -versioni 10 trovato in dotnet buildtools [più vicino di versione: 4.0.0-rc-2129]<br/> -versioni 9 trovato in NuGetVolatile [più vicino di versione: 3.0.0-beta-00032] <br/> -0 versioni, vedere dotnet core<br/> -0 versioni, vedere dotnet roslyn* |

### <a name="nu1104"></a>NU1104

| | |
| --- | --- |
| **Problema** | Un elemento ProjectReference punta a un file che non esiste. |
| **Cause più comuni** | Il file di progetto è presente sul disco o il riferimento non è corretto. |
| **Messaggio di esempio** | *Riferimento al progetto non esiste 'c:\a.csproj'. Verificare che il riferimento al progetto sia valido e che esista il file di progetto.* |

### <a name="nu1105"></a>NU1105

| | |
| --- | --- |
| **Problema** | Il file di progetto esiste ma è stata fornita alcuna informazione di ripristino per tale. |
| **Cause più comuni** | In Visual Studio ciò vuol dire che il progetto viene scaricato. Dalla riga di comando ciò vuol dire che il file è danneggiato o che non contenga personalizzata dopo la destinazione di importazioni necessarie per il ripristino leggere il progetto. |
| **Messaggio di esempio** | *Impossibile leggere le informazioni di progetto per 'c:\a.csproj'. Il file di progetto potrebbe essere destinazioni non valide o mancante necessarie per il ripristino.* |

### <a name="nu1106"></a>NU1106

| | |
| --- | --- |
| **Problema** | Vincoli di dipendenza non possono essere risolti. |
| **Cause più comuni** | I pacchetti contengono dipendenza versioni esatte di un pacchetto anziché intervalli aperti. |
| **Messaggio di esempio** | *Non è possibile soddisfare le richieste con conflitto per {id}: {percorso conflitto} Framework: {grafico di destinazione}* |

< name = "NU1107 ></a>

### <a name="nu1107-previously-nu1607"></a>NU1107 (in precedenza NU1607)

| | |
| --- | --- |
| **Problema** | Impossibile risolvere i vincoli di dipendenza tra pacchetti. |
| **Cause più comuni** | Pacchetti con vincoli di dipendenza in versioni esatte non consentono altri pacchetti per incrementare la versione, se necessario. |
| **Messaggio di esempio** | *Conflitto di versione per NuGet.Versioning. Fare riferimento il pacchetto direttamente dal progetto per risolvere il problema.<br/>  NuGet. Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (4.0.0 =)* |

< name = "NU1108 ></a>

### <a name="nu1108-previously-nu1606"></a>NU1108 (in precedenza NU1606)

| | |
| --- | --- |
| **Problema** | È stata rilevata una dipendenza circolare. |
| **Cause più comuni** | Un pacchetto viene creato in modo non corretto. |
| **Messaggio di esempio** | *Rilevato ciclo: A -> B -> A* |

## <a name="compatibility-errors"></a>Errori di compatibilità

[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)

### <a name="nu1201"></a>NU1201

| | |
| --- | --- |
| **Problema** | Una dipendenza di progetto non contiene un framework compatibile con il progetto corrente. |
| **Cause più comuni** | Il framework di destinazione del progetto è una versione successiva a quella del progetto consumer. |
| **Messaggio di esempio** | *Progetto ServerWeb non è compatibile con netstandard1.3 (. Moniker NETStandard, Version = v 1.3). Progetto supporta ServerWeb:<br/> -netstandard1.6 (. Moniker NETStandard, Version = v 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = v 1.0)* |

### <a name="nu1202"></a>NU1202

| | |
| --- | --- |
| **Problema** | Un pacchetto di dipendenze non contiene tutte le risorse compatibile con il progetto. |
| **Cause più comuni** | Il pacchetto non supporta il framework di destinazione del progetto. |
| **Messaggio di esempio** | *Pacchetto System.ComponentModel.EventBasedAsync 4.0.11 non è compatibile con netstandard1.3 (. Moniker NETStandard, Version = v 1.3). Creare il pacchetto supporta System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, Version = v 1.0)<br/> -monotouch10 (MonoTouch, Version = v 1.0)<br/> -net45 (. NETFramework, Version = v 4.5)<br/> -netcore50 (. NETCore, Version = v 5.0)<br/> -netstandard1.0 (. Moniker NETStandard, Version = v 1.0)<br/> -portabile net45 win8 wp8 + wpa81 (. NETPortable, versione = v0.0, profilo = Profile259)<br/> -win8 (Windows, Version = v 8.0)<br/> -wp8 (WindowsPhone, Version = v 8.0)<br/> -wpa81 (WindowsPhoneApp, Version = v 8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*|

### <a name="nu1203"></a>NU1203

| | |
| --- | --- |
| **Problema** | Il pacchetto non supporta il progetto `RuntimeIdentifier`. |
| **Cause più comuni** | Il pacchetto non supporta corrente `RuntimeIdentifier`. Modifica il `RuntimeIdentifier` valori usati nel progetto, se necessario. |
| **Messaggio di esempio** | *System.Example 1.0.0 fornisce un assembly di riferimento in fase di compilazione per DLL in net461, ma non sono presenti assembly di runtime compatibili.* |

### <a name="nu1401"></a>NU1401

| | |
| --- | --- |
| **Problema** | Il pacchetto richiede caratteristiche o Framework non sono attualmente supportati dalla versione installata di NuGet. |
| **Cause più comuni** | Aggiornare NuGet per risolvere il problema. |
| **Messaggio di esempio** | *Il pacchetto 'NuGet.Versioning' richiede '5.0.0' alla versione client NuGet o versione successiva, ma la versione NuGet corrente è '4.3.0'. Per aggiornare NuGet, vedere http://docs.nuget.org/consume/installing-nuget.* |

## <a name="invalid-input-warnings"></a>Avvisi di input non validi

[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)

### <a name="nu1501"></a>NU1501

| | |
| --- | --- |
| **Problema** | Il ripristino del progetto sta tentando di operare in non è stato trovato. |
| **Cause più comuni** | Il progetto è mancano. |
| **Messaggio di esempio** | *La cartella 'c:\projects\a' non contiene un progetto da ripristinare.* |

### <a name="nu1502"></a>NU1502

| | |
| --- | --- |
| **Problema** | `RuntimeSupports`contiene un profilo non valido. |
| **Cause più comuni** | Impossibile trovare il profilo supporta un `runtime.json` file dai pacchetti dipendenza corrente. |
| **Messaggio di esempio** | *Profilo di compatibilità sconosciuto: aaa* |

### <a name="nu1503"></a>NU1503

| | |
| --- | --- |
| **Problema** | Una dipendenza di progetto non importa le destinazioni di ripristino di NuGet. È simile a NU1105 ma qui il progetto viene ignorato e ignorato anziché causare tutte esito negativo del ripristino. Nelle soluzioni complesse sono spesso altri tipi di progetti che non supportano il ripristino. |
| **Cause più comuni** | Questa situazione può verificarsi per i progetti che non si importano props/destinazioni comuni quali l'importazione automatica di ripristino. Se il progetto non è necessaria per il ripristino può essere ignorato. |
| **Messaggio di esempio** | *Mancato ripristino per il progetto 'c:\a.csproj'. Il file di progetto potrebbe essere destinazioni non valide o mancante necessarie per il ripristino.* |

## <a name="unexpected-package-version-warnings"></a>Avvisi di versione di pacchetto imprevisto

[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)

### <a name="nu1601"></a>NU1601

| | |
| --- | --- |
| **Problema** | Una dipendenza diretta del progetto è stato ha respinto per una versione successiva a quella del progetto specificato. |
| **Cause più comuni** | Un altro pacchetto dipendenza necessaria una versione successiva e aumentata del pacchetto. |
| **Messaggio di esempio** | *Dipendenza specificata è NuGet.Versioning (> = 3.5.0) ma è risultata NuGet.Versioning 4.0.0.* |

### <a name="nu1602"></a>NU1602

| | |
| --- | --- |
| **Problema** | Una dipendenza pacchetto manca un limite inferiore. Questo non consente il ripristino trovare il *migliore corrispondenza*. Ogni ripristino verrà spostata verso il basso il tentativo di trovare una versione precedente che può essere utilizzata. Ciò significa che il ripristino passa nello stato online per controllare tutte le origini di ogni volta che invece di usare i pacchetti già esistenti nella cartella del pacchetto utente. |
| **Cause più comuni** | In genere si tratta di un pacchetto con errore di creazione. |
| **Messaggio di esempio** | *NuGet. Packaging 4.0.0 non prevede un limite inferiore inclusivo dipendenza NuGet.Versioning (3.5.0 >). Una corrispondenza migliore approssimativa di 3.6.0 è stato risolta.* |

### <a name="nu1603"></a>NU1603

| | |
| --- | --- |
| **Problema** | Una dipendenza pacchetto specificata una versione che non è stata trovata. È stata utilizzata una versione successiva, che differisce da cosa è stato creato il pacchetto base.<br/><br/>Ciò significa che il ripristino non è stata trovata la *migliore corrispondenza*. Ogni ripristino verrà spostata verso il basso il tentativo di trovare una versione precedente che può essere utilizzata. Ciò significa che il ripristino passa nello stato online per controllare tutte le origini di ogni volta che invece di usare i pacchetti già esistenti nella cartella del pacchetto utente. |
| **Cause più comuni** | Le origini del pacchetto non contengono la versione prevista limite inferiore. Se il pacchetto previsto non è stato rilasciato quindi potrebbe trattarsi di un pacchetto con errore di creazione. |
| **Messaggio di esempio** | NuGet. Packaging 4.0.0 dipende NuGet.Versioning (> = 4.0.0) 4.0.0 non è stato trovato. Una corrispondenza migliore approssimativa di 5.0.0 è stato risolta. |

### <a name="nu1604"></a>NU1604

| | |
| --- | --- |
| **Problema** | Dipendenza di progetto non viene definito un limite inferiore.<br/><br/>Ciò significa che il ripristino non è stata trovata la *migliore corrispondenza*. Ogni ripristino verrà spostata verso il basso il tentativo di trovare una versione precedente che può essere utilizzata. Ciò significa che il ripristino passa nello stato online per controllare tutte le origini di ogni volta che invece di usare i pacchetti già esistenti nella cartella del pacchetto utente. |
| **Cause più comuni** | Il progetto *PackageReference* *versione* attributo deve essere aggiornato per includere un limite inferiore. |
| **Messaggio di esempio** | *Progetto dipendenza NuGet.Versioning (< = 9.0.0) doe non contengono un limite inferiore inclusivo. Includere un limite inferiore nella versione di dipendenza per garantire risultati coerenti di ripristino.* |

### <a name="nu1605"></a>NU1605

| | |
| --- | --- |
| **Problema** | Un pacchetto di dipendenza è specificato un vincolo di versione in una versione superiore di un pacchetto rispetto al ripristino risolta. |
| **Cause più comuni** | Più vicino wins per la risoluzione dei pacchetti. Un pacchetto più vicini nel grafico può avere sottoposto a override un pacchetto distante. |
| **Messaggio di esempio** | *Rilevato downgrade del pacchetto: NuGet.Versioning da 4.0.0 a 3.5.0. Fare riferimento il pacchetto direttamente dal progetto per selezionare una versione diversa.<br/>  NuGet. Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0* |

## <a name="resolver-conflict-warnings"></a>Avvisi di sistema di risoluzione dei conflitti

[NU1608](#nu1608)

### <a name="nu1608"></a>NU1608

| | |
| --- | --- |
| **Problema** | Un pacchetto di risoluzione è supera a quello di un vincolo di dipendenza. In alcuni casi ciò è intenzionale e l'avviso può essere eliminato. |
| **Cause più comuni** | Un pacchetto a cui fa riferimento direttamente un progetto sostituiranno i vincoli di dipendenze da altri pacchetti.   |
| **Messaggio di esempio** | *Versione del pacchetto rilevato all'esterno di vincolo dipendenza: x 1.0.0 richiede y (= 1.0.0) ma versione 2.0.0 y è stato risolto.* |

## <a name="package-fallback-warnings"></a>Avvisi di fallback di pacchetto

[NU1701](#nu1701)

### <a name="nu1701"></a>NU1701

| | |
| --- | --- |
| **Problema** | *PackageTargetFallback/AssetTargetFallback* veniva utilizzato per selezionare asset da un pacchetto. Questo è un avviso per informare l'utente che le risorse potrebbero non essere compatibile al 100%. |
| **Cause più comuni** | Il pacchetto non supporta la struttura del progetto. |
| **Messaggio di esempio** | *Pacchetto 'NuGet.Versioning' è stato ripristinato mediante 'portable net45 + win8' invece del framework di destinazione del progetto 'netstandard1.5'. Questo pacchetto potrebbe non essere completamente compatibile con il progetto.* |

## <a name="feed-warnings"></a>Feed di avvisi

[NU1801](#nu1801)

### <a name="nu1801"></a>NU1801

| | |
| --- | --- |
| **Problema** | Si è verificato un errore durante la lettura dei feed quando `IgnoreFailedSources` è impostata su true, convertendolo in un messaggio di avviso non irreversibile. Ciò può contenere qualsiasi messaggio ed è generico. |
| **Cause più comuni** | L'origine non è valido. |
| **Messaggio di esempio** | N/D |

## <a name="nuget-internal-errors-and-warnings"></a>Avvisi ed errori interni di NuGet

[NU1000](#nu1000) | [NU1500](#nu1500)

### <a name="nu1000"></a>NU1000

| | |
| --- | --- |
| **Problema** | Un errore interno non specifico da NuGet. |
| **Cause più comuni** | Controllare i registri per ulteriori informazioni |

### <a name="nu1500"></a>NU1500

| | |
| --- | --- |
| **Problema** | Un avviso interno non specifico da NuGet. |
| **Cause più comuni** | Controllare i registri per ulteriori informazioni |
