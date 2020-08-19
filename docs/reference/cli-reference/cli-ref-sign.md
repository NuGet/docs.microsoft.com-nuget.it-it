---
title: Comando firma CLI NuGet
description: Riferimento per il comando nuget.exe Sign
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622772"
---
# <a name="sign-command-nuget-cli"></a>comando Sign (interfaccia della riga di comando NuGet)

**Si applica a:** versioni supportate per la creazione di pacchetti &bullet; **:** 4.6 +

Firma tutti i pacchetti che corrispondono al primo argomento con un certificato. Il certificato con la chiave privata può essere ottenuto da un file o da un certificato installato in un archivio certificati fornendo un nome soggetto o un'identificazione personale.

> [!Note]
> La firma del pacchetto non è ancora supportata in .NET Core, in mono o in piattaforme non Windows.

## <a name="usage"></a>Uso

```cli
nuget sign <package(s)> [options]
```

dove `<package(s)>` è uno o più `.nupkg` file.

## <a name="options"></a>Opzioni

- **`-CertificateFingerprint`**

  Specifica l'impronta digitale SHA-1 del certificato utilizzato per eseguire la ricerca in un archivio certificati locale per il certificato.

- **`-CertificatePassword`**

  Specifica la password del certificato, se necessario. Se un certificato è protetto da password ma non viene fornita alcuna password, il comando richiederà una password in fase di esecuzione, a meno che non `-NonInteractive` venga passata l'opzione.

- **`-CertificatePath`**

  Specifica il percorso del file del certificato da utilizzare per la firma del pacchetto.

- **`-CertificateStoreLocation`**

  Specifica il nome dell'archivio certificati X. 509 utilizzato per cercare il certificato. Il valore predefinito è "CurrentUser", l'archivio certificati X. 509 utilizzato dall'utente corrente. Questa opzione deve essere usata quando si specifica il certificato tramite le `-CertificateSubjectName` `-CertificateFingerprint` Opzioni o.

- **`-CertificateStoreName`**

  Specifica il nome dell'archivio certificati X. 509 da utilizzare per la ricerca del certificato. Il valore predefinito è "My", l'archivio certificati X. 509 per i certificati personali. Questa opzione deve essere usata quando si specifica il certificato tramite le `-CertificateSubjectName` `-CertificateFingerprint` Opzioni o.

- **`-CertificateSubjectName`**

  Specifica il nome del soggetto del certificato utilizzato per eseguire la ricerca in un archivio certificati locale per il certificato.  La ricerca è un confronto tra stringhe senza distinzione tra maiuscole e minuscole usando il valore fornito, che troverà tutti i certificati con il nome del soggetto che contiene tale stringa, indipendentemente dagli altri valori dell'oggetto.  L'archivio certificati può essere specificato dalle `-CertificateStoreName` `-CertificateStoreLocation` Opzioni e.

- **`-ConfigFile`**

  File di configurazione NuGet da applicare. Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.

- **`-HashAlgorithm`**

  Algoritmo hash da utilizzare per firmare il pacchetto. Il valore predefinito è SHA256. I valori possibili sono SHA256, SHA384 e SHA512.

- **`-?|-help`**

  Visualizza le informazioni della Guida per il comando.

- **`-NonInteractive`**

  Evita la richiesta di input o conferme dell'utente.

- **`-OutputDirectory`**

  Specifica la directory in cui deve essere salvato il pacchetto firmato. Per impostazione predefinita, il pacchetto originale viene sovrascritto dal pacchetto firmato.

- **`-Overwrite`**

  Opzione per indicare se la firma corrente deve essere sovrascritta. Per impostazione predefinita, il comando avrà esito negativo se il pacchetto dispone già di una firma.

- **`-Timestamper`**

  URL di un server di timestamp RFC 3161.

- **`-TimestampHashAlgorithm`**

  Algoritmo hash che verrà usato dal server di timestamp RFC 3161. Il valore predefinito è SHA256.

- **`-Verbosity [normal|quiet|detailed]`**

  Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .

## <a name="examples"></a>Esempi

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
