---
title: NuGet errori e avvisi riferimento
description: Riferimento complete per avvisi ed errori generati da NuGet durante le varie operazioni di NuGet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: anangaur
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: dcff20e35adc0a3dbcc7bef482f81a937cf059c5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="errors-and-warnings"></a>Errori e avvisi

In NuGet 4.3.0+, errori e avvisi sono numerati come descritto in questo argomento e forniscono informazioni dettagliate che consentono di risolvere i problemi che interessano.

Gli errori e avvisi elencati di seguito sono disponibili solo con [basato su PackageReference](../consume-packages/package-references-in-project-files.md) 4.3.0+ NuGet e progetti. NuGet anche rispetta la proprietà di MSBuild per l'esclusione di avvisi o li elevare a errori. Per ulteriori informazioni, vedere [procedura: esclusione di avvisi del compilatore](/visualstudio/ide/how-to-suppress-compiler-warnings) nella documentazione di Visual Studio.

**Errori**

| Gruppo | Numeri di errore |
| --- | --- |
| [Errori di input non validi](#invalid-input-errors) | [NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003) |
| [Errori di pacchetto e progetto mancanti](#missing-package-and-project-errors) | [NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (in precedenza NU1607), [NU1108](#nu1108) (in precedenza NU1606) |
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
| [Pacchetti firmati (creazione e la verifica)](#signed-packages-creation-and-verification)| [NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028) |

## <a name="invalid-input-errors"></a>Errori di input non validi

[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)

### <a name="nu1001"></a>NU1001

| | |
| --- | --- |
| **Problema** | Il progetto non contiene uno o più Framework. |
| **Messaggio di esempio** | *ProjA il progetto non specifica alcun framework di destinazione in c:\tmp\projA.csproj* |
| **Soluzione** | Aggiungere un `TargetFramework` o `TargetFrameworks` proprietà al file di progetto specificato. |

### <a name="nu1002"></a>NU1002

| | |
| --- | --- |
| **Problema** | Combinazione non valida di input con una parola chiave non CRITTOGRAFATO. |
| **Messaggio di esempio** | *'CLEAR' non può essere utilizzato in combinazione con altri valori* |
| **Soluzione** | Usare deselezionare singolarmente e omettere tutti gli altri input. |

### <a name="nu1003"></a>NU1003

| | |
| --- | --- |
| **Problema** | `PackageTargetFallback` e `AssetTargetFallback` comportamenti diversi per la selezione di risorse e non possono essere utilizzati insieme. |
| **Messaggio di esempio** | *PackageTargetFallback e AssetTargetFallback non possono essere utilizzati insieme. Rimuovere i riferimenti di PackageTargetFallback(deprecated) dall'ambiente del progetto.* |
| **Soluzione** | Rimuovere deprecate `PackageTargetFallback` elemento dal progetto. |

## <a name="missing-package-and-project-errors"></a>Errori di pacchetto e progetto mancanti

[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)

### <a name="nu1100"></a>NU1100

| | |
| --- | --- |
| **Problema** | Un gruppo di dipendenze non essere risolto. Questo è un problema generico per tipi che non sono pacchetti o progetti. |
| **Messaggio di esempio** | *Impossibile risolvere System.Missing per net45* |
| **Soluzione** | Aprire il file di progetto ed esaminare l'elenco delle relative dipendenze. Verificare che ogni dipendenza presente per le origini del pacchetto in uso e che il pacchetto supporta il framework di destinazione del progetto. |

### <a name="nu1101"></a>NU1101

| | |
| --- | --- |
| **Problema** | Impossibile trovare il pacchetto su tutte le origini. |
| **Messaggio di esempio** | *Impossibile trovare il pacchetto System.Missing. Nessun pacchetto esistenti con questo id nelle origini: dotnet-core, dotnet roslyn, nuget.org* |
| **Soluzione** | Esaminare le dipendenze del progetto in Visual Studio per verificare che il pacchetto corretto identificatore e numero di versione in uso. Controllare inoltre che il [configurazione NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifica l'origine del pacchetto il prevede di utilizzare. Se si utilizzano pacchetti contenenti [controllo delle versioni semantico 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), assicurarsi che si sta utilizzando il [V3 feed](https://api.nuget.org/v3/index.json) nel [configurazione NuGet](../consume-packages/Configuring-NuGet-Behavior.md). |

### <a name="nu1102"></a>NU1102

| | |
| --- | --- |
| **Problema** | L'identificatore del pacchetto è stato trovato ma presente una versione all'interno dell'intervallo di dipendenza specificata non può essere una delle origini. L'intervallo può essere specificato da un pacchetto e non dell'utente. |
| **Messaggio di esempio** | *Impossibile trovare il pacchetto NuGet.Versioning con la versione (> = 9.0.1)<br/> -30 trovare versioni in nuget.org [più vicino di versione: 4.0.0]<br/> -versioni 10 trovato in dotnet buildtools [più vicino di versione: 4.0.0-rc-2129]<br/> -9 trovato versioni in NuGetVolatile [più vicino di versione: 3.0.0-beta-00032]<br/> -0 versioni, vedere dotnet core<br/> -0 versioni, vedere dotnet roslyn* |
| **Soluzione** | Modificare il file di progetto per risolvere la versione del pacchetto. Controllare inoltre che il [configurazione NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifica l'origine del pacchetto il prevede di utilizzare. Potrebbe essere necessario modificare la versione requeted se il pacchetto fa riferimento direttamente il progetto. |

### <a name="nu1103"></a>NU1103

| | |
| --- | --- |
| **Problema** | Il progetto specificato una versione stabile per l'intervallo di dipendenza, ma nessuna versione stabile trovata in tale intervallo. Le versioni non definitive sono state trovate, ma non sono consentite. |
| **Messaggio di esempio** | *Impossibile trovare un pacchetto stabile NuGet.Versioning con la versione (> = 3.0.0)<br/> -versioni 10 trovato in dotnet buildtools [più vicino di versione: 4.0.0-rc-2129]<br/> -versioni 9 trovato in NuGetVolatile [più vicino di versione: 3.0.0-beta-00032] <br/> -0 versioni, vedere dotnet core<br/> -0 versioni, vedere dotnet roslyn* |
| **Soluzione** |  Modificare l'intervallo di versione nel file di progetto per includere le versioni non definitive. Vedere [il controllo delle versioni di pacchetto](../reference/Package-Versioning.md). |

### <a name="nu1104"></a>NU1104

| | |
| --- | --- |
| **Problema** | Un elemento ProjectReference punta a un file che non esiste. |
| **Messaggio di esempio** | *Riferimento al progetto non esiste 'c:\a.csproj'. Verificare che il riferimento al progetto sia valido e che esista il file di progetto.* |
| **Soluzione** | Modificare il file di progetto per correggere il percorso per il progetto di riferimento o per rimuovere il riferimento all'elemento se non è più necessario. |

### <a name="nu1105"></a>NU1105

| | |
| --- | --- |
| **Problema** | Il file di progetto esiste ma è stata fornita alcuna informazione di ripristino per tale. |
| **Messaggio di esempio** | *Impossibile leggere le informazioni di progetto per 'c:\a.csproj'. Il file di progetto potrebbe essere destinazioni non valide o mancante necessarie per il ripristino.* |
| **Soluzione** | In Visual Studio, l'errore potrebbe indicare che il progetto viene scaricato, nel qual caso ricaricare il progetto. Dalla riga di comando ciò vuol dire che il file è danneggiato o che non contenga personalizzata "dopo l'importazione" necessarie per il ripristino leggere il progetto di destinazione. Verificare che il file di progetto sia valido e contiene una destinazione "dopo l'importazione". |

### <a name="nu1106"></a>NU1106

| | |
| --- | --- |
| **Problema** | Vincoli di dipendenza non possono essere risolti. |
| **Messaggio di esempio** | *Non è possibile soddisfare le richieste con conflitto per {id}: {percorso conflitto} Framework: {grafico di destinazione}* |
| **Soluzione** | Modificare il file di progetto per specificare gli intervalli di più flessibile per la dipendenza anziché la versione esatta. |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a>NU1107 (in precedenza NU1607)

| | |
| --- | --- |
| **Problema** | Impossibile risolvere i vincoli di dipendenza tra pacchetti. |
| **Messaggio di esempio** | *Conflitto di versione per NuGet.Versioning. Fare riferimento il pacchetto direttamente dal progetto per risolvere il problema.<br/>  NuGet. Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)* |
| **Soluzione** | Pacchetti con vincoli di dipendenza in versioni esatte non consentono altri pacchetti per incrementare la versione, se necessario. Aggiungere un riferimento al progetto direttamente (nel file di progetto) con la versione esatta richiesta. |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a>NU1108 (in precedenza NU1606)

| | |
| --- | --- |
| **Problema** | È stata rilevata una dipendenza circolare. |
| **Messaggio di esempio** | *Rilevato ciclo: A -> B -> A* |
| **Soluzione** | Il pacchetto sia stato creato in modo errato. contattare il proprietario del pacchetto per correggere il bug. |

## <a name="compatibility-errors"></a>Errori di compatibilità

[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)

### <a name="nu1201"></a>NU1201

| | |
| --- | --- |
| **Problema** | Una dipendenza di progetto non contiene un framework compatibile con il progetto corrente. In genere, il framework di destinazione del progetto è una versione successiva a quella del progetto consumer. |
| **Messaggio di esempio** | *Progetto ServerWeb non è compatibile con netstandard1.3 (. Moniker NETStandard, Version = v 1.3). Progetto supporta ServerWeb:<br/> -netstandard1.6 (. Moniker NETStandard, Version = v 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = v 1.0)* |
| **Soluzione** | Modificare il framework di destinazione del progetto a una versione uguale o inferiore a quella del progetto consumer. |

### <a name="nu1202"></a>NU1202

| | |
| --- | --- |
| **Problema** | Un pacchetto di dipendenze non contiene tutte le risorse compatibile con il progetto. |
| **Messaggio di esempio** | *Pacchetto System.ComponentModel.EventBasedAsync 4.0.11 non è compatibile con netstandard1.3 (. Moniker NETStandard, Version = v 1.3). Creare il pacchetto supporta System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, Version = v 1.0)<br/> -monotouch10 (MonoTouch, Version = v 1.0)<br/> -net45 (. NETFramework, Version = v 4.5)<br/> -netcore50 (. NETCore, Version = v 5.0)<br/> -netstandard1.0 (. Moniker NETStandard, Version = v 1.0)<br/> -portabile net45 win8 wp8 + wpa81 (. NETPortable, versione = v0.0, profilo = Profile259)<br/> -win8 (Windows, Version = v 8.0)<br/> -wp8 (WindowsPhone, Version = v 8.0)<br/> -wpa81 (WindowsPhoneApp, Version = v 8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*|
| **Soluzione** | Modificare il framework di destinazione del progetto in modo che il pacchetto supporta. |

### <a name="nu1203"></a>NU1203

| | |
| --- | --- |
| **Problema** | Il pacchetto non supporta il progetto `RuntimeIdentifier`. |
| **Messaggio di esempio** | *System.Example 1.0.0 fornisce un assembly di riferimento in fase di compilazione per DLL in net461, ma non sono presenti assembly di runtime compatibili.* |
| **Soluzione** | Modifica il `RuntimeIdentifier` valori usati nel progetto in base alle esigenze. |

### <a name="nu1401"></a>NU1401

| | |
| --- | --- |
| **Problema** | Il pacchetto richiede caratteristiche o Framework non sono attualmente supportati dalla versione installata di NuGet. |
| **Messaggio di esempio** | *Il pacchetto 'NuGet.Versioning' richiede '5.0.0' alla versione client NuGet o versione successiva, ma la versione NuGet corrente è '4.3.0'.* |
| **Soluzione** | Installare una versione più recente di NuGet. Vedere [gli strumenti client di installazione di NuGet](../install-nuget-client-tools.md). |

## <a name="invalid-input-warnings"></a>Avvisi di input non validi

[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)

### <a name="nu1501"></a>NU1501

| | |
| --- | --- |
| **Problema** | Il ripristino del progetto sta tentando di operare in non è stato trovato. |
| **Messaggio di esempio** | *La cartella 'c:\projects\a' non contiene un progetto da ripristinare.* |
| **Soluzione** | Esegue nuget restore in una cartella che contiene un progetto. |

### <a name="nu1502"></a>NU1502

| | |
| --- | --- |
| **Problema** | `RuntimeSupports` contiene un profilo non valido. In genere, il profilo supporta non è stato trovato un `runtime.json` file dai pacchetti dipendenza corrente.|
| **Messaggio di esempio** | *Profilo di compatibilità sconosciuto: aaa* |
| **Soluzione** | Controllare il `RuntimeSupports` valore nel progetto. |

### <a name="nu1503"></a>NU1503

| | |
| --- | --- |
| **Problema** | Una dipendenza di progetto non importa le destinazioni di ripristino di NuGet. È simile a NU1105 ma qui il progetto viene ignorato e ignorato anziché causare tutte esito negativo del ripristino. Nelle soluzioni complesse sono spesso altri tipi di progetti che non supportano il ripristino. |
| **Messaggio di esempio** | *Mancato ripristino per il progetto 'c:\a.csproj'. Il file di progetto potrebbe essere destinazioni non valide o mancante necessarie per il ripristino.* |
| **Soluzione** | Questa situazione può verificarsi per i progetti che non si importano props/destinazioni comuni quali l'importazione automatica di ripristino. Se il progetto non è necessaria per il ripristino può essere ignorato. In caso contrario, modificare il progetto interessato per aggiungere destinazioni per il ripristino. |

## <a name="unexpected-package-version-warnings"></a>Avvisi di versione di pacchetto imprevisto

[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)

### <a name="nu1601"></a>NU1601

| | |
| --- | --- |
| **Problema** | Una dipendenza diretta del progetto è stato ha respinto per una versione successiva a quella del progetto specificato. |
| **Messaggio di esempio** | *Dipendenza specificata è NuGet.Versioning (> = 3.5.0) ma è risultata NuGet.Versioning 4.0.0.* |
| **Soluzione** | Aggiornare la dipendenza nel progetto a una versione appropriata. |

### <a name="nu1602"></a>NU1602

| | |
| --- | --- |
| **Problema** | Una dipendenza pacchetto manca un limite inferiore. Questo non consente il ripristino trovare il *migliore corrispondenza*. Ogni ripristino verrà spostata verso il basso il tentativo di trovare una versione precedente che può essere utilizzata. Ciò significa che il ripristino passa nello stato online per controllare tutte le origini di ogni volta che invece di usare i pacchetti già esistenti nella cartella del pacchetto utente. |
| **Messaggio di esempio** | *NuGet. Packaging 4.0.0 non prevede un limite inferiore inclusivo dipendenza NuGet.Versioning (3.5.0 >). Una corrispondenza migliore approssimativa di 3.6.0 è stato risolta.* |
| **Soluzione** | In genere si tratta di un pacchetto con errore di creazione. Contattare l'autore del pacchetto per risolvere il problema. |

### <a name="nu1603"></a>NU1603

| | |
| --- | --- |
| **Problema** | Una dipendenza pacchetto specificata una versione che non è stata trovata. In genere, le origini del pacchetto non contengono la versione prevista limite inferiore. È stata utilizzata una versione successiva, che differisce da cosa è stato creato il pacchetto base.<br/><br/>Ciò significa che il ripristino non è stata trovata la *migliore corrispondenza*. Ogni ripristino verrà spostata verso il basso il tentativo di trovare una versione precedente che può essere utilizzata. Ciò significa che il ripristino passa nello stato online per controllare tutte le origini di ogni volta che invece di usare i pacchetti già esistenti nella cartella del pacchetto utente. |
| **Messaggio di esempio** | NuGet. Packaging 4.0.0 dipende NuGet.Versioning (> = 4.0.0) 4.0.0 non è stato trovato. Una corrispondenza migliore approssimativa di 5.0.0 è stato risolta. |
| **Soluzione** | Se il pacchetto previsto non è stato rilasciato quindi potrebbe trattarsi di un pacchetto con errore di creazione. Contattare l'autore del pacchetto per risolvere il problema. Se il pacchetto è stato rilasciato, controllare che sia disponibile per le origini del pacchetto in uso. Se si utilizza un'origine privata, si potrebbe essere necessario aggiornare il pacchetto su tale feed. |

### <a name="nu1604"></a>NU1604

| | |
| --- | --- |
| **Problema** | Dipendenza di progetto non viene definito un limite inferiore.<br/><br/>Ciò significa che il ripristino non è stata trovata la *migliore corrispondenza*. Ogni ripristino verrà spostata verso il basso il tentativo di trovare una versione precedente che può essere utilizzata. Ciò significa che il ripristino passa nello stato online per controllare tutte le origini di ogni volta che invece di usare i pacchetti già esistenti nella cartella del pacchetto utente. |
| **Messaggio di esempio** | *Progetto dipendenza NuGet.Versioning (< = 9.0.0) doe non contengono un limite inferiore inclusivo. Includere un limite inferiore nella versione di dipendenza per garantire risultati coerenti di ripristino.* |
| **Soluzione** | Aggiornare il progetto `PackageReference` `Version` attributo da includere un limite inferiore. |

### <a name="nu1605"></a>NU1605

| | |
| --- | --- |
| **Problema** | Un pacchetto di dipendenza è specificato un vincolo di versione in una versione superiore di un pacchetto rispetto al ripristino risolta. Ovvero "più vicino wins" regola per la risoluzione dei pacchetti, a causa di un pacchetto più vicini nel grafico può avere sottoposto a override un pacchetto distante. |
| **Messaggio di esempio** | *Rilevato downgrade del pacchetto: NuGet.Versioning da 4.0.0 a 3.5.0. Fare riferimento il pacchetto direttamente dal progetto per selezionare una versione diversa.<br/>  NuGet. Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0* |
| **Soluzione** | Aggiungere un riferimento diretto al progetto per la successiva versione del pacchetto che si desidera utilizzare. |

## <a name="resolver-conflict-warnings"></a>Avvisi di sistema di risoluzione dei conflitti

### <a name="nu1608"></a>NU1608

| | |
| --- | --- |
| **Problema** | Un pacchetto risolto è supera a quello di un vincolo di dipendenza. Ciò significa che un pacchetto a cui fa riferimento direttamente un progetto ignora i vincoli di dipendenze da altri pacchetti.|
| **Messaggio di esempio** | *Versione del pacchetto rilevato all'esterno di vincolo dipendenza: x 1.0.0 richiede y (= 1.0.0) ma versione 2.0.0 y è stato risolto.* |
| **Soluzione** | In alcuni casi ciò è intenzionale e l'avviso può essere eliminato. In caso contrario, modificare il riferimento del progetto al pacchetto per ampliare i vincoli di versione. |

## <a name="package-fallback-warnings"></a>Avvisi di fallback di pacchetto

### <a name="nu1701"></a>NU1701

| | |
| --- | --- |
| **Problema** | `PackageTargetFallback` / `AssetTargetFallback` è stato usato per selezionare asset da un pacchetto. Avviso di informerà gli utenti che le risorse potrebbero non essere compatibile al 100%. |
| **Messaggio di esempio** | *Pacchetto 'NuGet.Versioning' è stato ripristinato mediante 'portable net45 + win8' invece del framework di destinazione del progetto 'netstandard1.5'. Questo pacchetto potrebbe non essere completamente compatibile con il progetto.* |
| **Soluzione** | Modificare il framework di destinazione del progetto in modo che il pacchetto supporta. |

## <a name="feed-warnings"></a>Feed di avvisi

### <a name="nu1801"></a>NU1801

| | |
| --- | --- |
| **Problema** | Si è verificato un errore durante la lettura dei feed quando `IgnoreFailedSources` è impostata su true, convertendolo in un messaggio di avviso non irreversibile. Ciò può contenere qualsiasi messaggio ed è generico. |
| **Messaggio di esempio** | N/D |
| **Soluzione** | Modificare la configurazione per specificare le origini valide. |

## <a name="nuget-internal-errors-and-warnings"></a>Avvisi ed errori interni di NuGet

[NU1000](#nu1000) | [NU1500](#nu1500)

### <a name="nu1000"></a>NU1000

| | |
| --- | --- |
| **Problema** | Un errore interno non specifico da NuGet. |
| **Soluzione** | Controllare i registri per ulteriori informazioni |

### <a name="nu1500"></a>NU1500

| | |
| --- | --- |
| **Problema** | Un avviso interno non specifico da NuGet. |
| **Soluzione** | Controllare i registri per ulteriori informazioni |

## <a name="signed-packages-creation-and-verification"></a>Pacchetti firmati (creazione e la verifica)

*4.6.0+ NuGet*

[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)

### <a name="nu3000"></a>NU3000

| | |
| --- | --- |
| **Problema** | Un errore non specifico relativo alla firma del pacchetto e firmati verifica del pacchetto. |
| **Soluzione** | Controllare i registri per ulteriori informazioni. |

### <a name="nu3001"></a>NU3001

| | |
| --- | --- |
| **Problema** | Argomenti non validi a uno di [firmare comando](../tools/cli-ref-sign.md) o [verificare comando](../tools/cli-ref-verify.md). |
| **Soluzione** | Controllare e correggere gli argomenti forniti. |

### <a name="nu3002"></a>NU3002

| | |
| --- | --- |
| **Problema** | Il `-Timestamper` non è stata specificata con il [comando sign nuget](../tools/cli-ref-sign.md). |
| **Messaggio di esempio** | *Il '-Timestamper' opzione non è stato specificato. Il pacchetto firmato non saranno impostati i timestamp.* |
| **Soluzione** | Specificare il `-Timestamper` con `nuget sign`. |

### <a name="nu3004"></a>NU3004

| | |
| --- | --- |
| **Problema** | È stato fornito un pacchetto non firmato per il [nuget verificare comando](../tools/cli-ref-verify.md). |
| **Soluzione** | Eseguire `nuget verify` con un pacchetto firmato. Vedere [firmare un pacchetto](../create-packages/Sign-a-Package.md). |

### <a name="nu3008"></a>NU3008

| | |
| --- | --- |
| **Problema** | Il pacchetto non riuscito, vale a dire che un pacchetto firmato sia stato manomesso dopo l'accesso. |
| **Soluzione** | Scansione del computer con un software antivirus. Quindi rimuovere il pacchetto dal computer, reinstallarlo e riprovare. Se il problema persiste, contattare il proprietario dell'origine del pacchetto e il proprietario del pacchetto. |

### <a name="nu3018"></a>NU3018

| | |
| --- | --- |
| **Problema** | Non è riuscita la creazione della catena di certificati per la firma primaria. Il certificato di firma primario non è attendibile, revocato, o informazioni di revoca per il certificato non sono disponibile. |
| **Messaggio di esempio** | *Avviso: NU3018: la funzione di revoca non è riuscita a controllare la revoca del certificato.* |
| **Soluzione** | Usare un certificato attendibile e valido. Verificare la connettività internet. |

### <a name="nu3028"></a>NU3028

| | |
| --- | --- |
| **Problema** | Non è riuscita la creazione della catena di certificati per la firma del timestamp. Il certificato di firma del timestamp non è attendibile, revocato, o informazioni di revoca per il certificato non sono disponibile. |
| **Messaggio di esempio** | *Avviso: NU3028: la funzione di revoca non è riuscita a controllare la revoca del certificato.* |
| **Soluzione** | Usare un certificato attendibile e valido. Verificare la connettività internet. |
