---
title: Comando firma CLI NuGet
description: Riferimento per il comando di firma NuGet. exe
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 746f7a421bd855b77716388b4af2fecbd5cf5a68
ms.sourcegitcommit: 96aab8a1ad35eca0c029679d0158d9cc93d66009
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/06/2020
ms.locfileid: "75676406"
---
# <a name="sign-command-nuget-cli"></a>Comando sign (interfaccia della riga di comando di NuGet)

**Si applica a: creazione di** pacchetti &bullet; **versioni supportate:** 4.6 +

Firma tutti i pacchetti che corrispondono al primo argomento con un certificato. Il certificato con la chiave privata può essere ottenuto da un file o da un certificato installato in un archivio certificati fornendo un nome soggetto o un'identificazione personale.

> [!Note]
> La firma del pacchetto non è ancora supportata in .NET Core, in mono o in piattaforme non Windows.

## <a name="usage"></a>Usage

```cli
nuget sign <package(s)> [options]
```

dove `<package(s)>` è uno o più file di `.nupkg`.

## <a name="options"></a>Options

| Opzione | Descrizione |
| --- | --- |
| CertificateFingerprint | Specifica l'impronta digitale SHA-1 del certificato utilizzato per eseguire la ricerca in un archivio certificati locale per il certificato. |
| CertificatePassword | Specifica la password del certificato, se necessario. Se un certificato è protetto da password ma non viene fornita alcuna password, il comando richiederà una password in fase di esecuzione, a meno che non venga passata l'opzione-Interactive. |
| CertificatePath | Specifica il percorso del file del certificato da utilizzare per la firma del pacchetto. |
| CertificateStoreLocation | Specifica il nome dell'archivio certificati X. 509 utilizzato per cercare il certificato. Il valore predefinito è "CurrentUser", l'archivio certificati X. 509 utilizzato dall'utente corrente. Questa opzione deve essere usata quando si specifica il certificato tramite le opzioni-CertificateSubjectName o-CertificateFingerprint. |
| CertificateStoreName | Specifica il nome dell'archivio certificati X. 509 da utilizzare per la ricerca del certificato. Il valore predefinito è "My", l'archivio certificati X. 509 per i certificati personali. Questa opzione deve essere usata quando si specifica il certificato tramite le opzioni-CertificateSubjectName o-CertificateFingerprint. |
| CertificateSubjectName | Specifica il nome del soggetto del certificato utilizzato per eseguire la ricerca in un archivio certificati locale per il certificato.  La ricerca è un confronto tra stringhe senza distinzione tra maiuscole e minuscole usando il valore fornito, che troverà tutti i certificati con il nome del soggetto che contiene tale stringa, indipendentemente dagli altri valori dell'oggetto.  L'archivio certificati può essere specificato tramite le opzioni-NomeArchivioCertificati e-CertificateStoreLocation. |
| ConfigFile | File di configurazione NuGet da applicare. Se non specificato, viene usato `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| ForceEnglishOutput | Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese. |
| HashAlgorithm | Algoritmo hash da utilizzare per firmare il pacchetto. Il valore predefinito è SHA256. |
| Guida di | Visualizza le informazioni della Guida per il comando. |
| NonInteractive | Evita la richiesta di input o conferme dell'utente. |
| OutputDirectory | Specifica la directory in cui deve essere salvato il pacchetto firmato. Per impostazione predefinita, il pacchetto originale viene sovrascritto dal pacchetto firmato. |
| Overwrite | Opzione per indicare se la firma corrente deve essere sovrascritta. Per impostazione predefinita, il comando avrà esito negativo se il pacchetto dispone già di una firma. |
| Timestamp | URL di un server di timestamp RFC 3161. |
| TimestampHashAlgorithm | Algoritmo hash che verrà usato dal server di timestamp RFC 3161. Il valore predefinito è SHA256. |
| Livello di dettaglio | Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*. |

## <a name="examples"></a>Esempi

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
