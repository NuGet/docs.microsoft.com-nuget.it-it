---
title: Comando sign NuGet CLI
description: Riferimento per il comando di accesso di nuget.exe
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7e84d794b802cfd69c785f720280fd5c022a46f6
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="sign-command-nuget-cli"></a>comando Sign (NuGet CLI)

**Si applica a:** creazione di pacchetti &bullet; **le versioni supportate:** 4.6 +

Tutti i pacchetti corrispondenti il primo argomento con un certificato di firma. Il certificato con la chiave privata può essere ottenuto da un file o da un certificato installato in un archivio certificati, fornendo un nome soggetto o un'identificazione personale.

Firmare il pacchetto non è ancora supportato in .NET Core, in Mono o su piattaforme non Windows.

## <a name="usage"></a>Utilizzo

```cli
nuget sign <package(s)> [options]
```

dove `<package(s)>` uno o più `.nupkg` file.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| CertificateFingerprint | Specifica l'impronta digitale SHA-1 del certificato utilizzato per la ricerca di un archivio certificati locale il certificato. |
| CertificatePassword | Specifica la password del certificato, se necessario. Se un certificato è protetto da password, ma non viene fornita alcuna password, il comando richiederà una password in fase di esecuzione, a meno che non-opzione interattiva viene passato. |
| CertificatePath | Specifica il percorso del file per il certificato da utilizzare nella firma del pacchetto. |
| CertificateStoreLocation | Specifica il nome di utilizzo di archivio del certificato x. 509 per la ricerca del certificato. Il valore predefinito "CurrentUser", l'archivio di certificati x. 509 utilizzato dall'utente corrente. Questa opzione deve essere utilizzata quando si specifica il certificato tramite le opzioni - CertificateSubjectName o - CertificateFingerprint. |
| CertificateStoreName | Specifica il nome dell'archivio certificati x. 509 da utilizzare per cercare il certificato. Valore predefinito è "My", l'archivio di certificati x. 509 per certificati personali. Questa opzione deve essere utilizzata quando si specifica il certificato tramite le opzioni - CertificateSubjectName o - CertificateFingerprint. |
| CertificateSubjectName | Specifica il nome del soggetto del certificato utilizzato per la ricerca di un archivio certificati locale il certificato.  La ricerca è un confronto di stringhe tra maiuscole e minuscole utilizzando il valore specificato, che consentirà di trovare tutti i certificati con il nome del soggetto che contiene tale stringa, indipendentemente dagli altri valori dell'oggetto.  L'archivio certificati può essere specificato dalle opzioni NomeArchivioCertificati - e - CertificateStoreLocation. |
| ConfigFile | Il file di configurazione NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.|
| ForceEnglishOutput | Nuget.exe forza l'esecuzione utilizzando le impostazioni cultura invariante, in lingua inglese. |
| HashAlgorithm | Algoritmo hash da usare per firmare il pacchetto. Valore predefinito è SHA256. |
| ? | Visualizza la Guida informazioni per il comando. |
| Non interattivo | Elimina richieste per l'input dell'utente o le conferme. |
| OutputDirectory | Specifica la directory in cui salvare il pacchetto firmato. Per impostazione predefinita, il pacchetto originale viene sovrascritto con il pacchetto firmato. |
| Overwrite | Opzione per indicare se la firma corrente deve essere sovrascritti. Per impostazione predefinita il comando avrà esito negativo se il pacchetto contiene già una firma. |
| Timestamper | URL a un server di timestamp RFC 3161. |
| TimestampHashAlgorithm | Algoritmo hash da usare dal server di timestamp RFC 3161. Valore predefinito è SHA256. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |

## <a name="examples"></a>Esempi

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```