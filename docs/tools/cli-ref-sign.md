---
title: Comando di NuGet CLI sign
description: Informazioni di riferimento per il comando di accesso nuget.exe
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546363"
---
# <a name="sign-command-nuget-cli"></a>Comando sign (interfaccia della riga di comando di NuGet)

**Si applica a:** creazione del pacchetto &bullet; **le versioni supportate:** 4.6 e versioni successive

Firma tutti i pacchetti corrispondenti il primo argomento con un certificato. Il certificato con la chiave privata può essere ottenuto da un file o da un certificato installato in un archivio certificati, fornendo un nome soggetto o un'identificazione personale.

La firma del pacchetto non è ancora supportata in .NET Core, in Mono, o su piattaforme non Windows.

## <a name="usage"></a>Utilizzo

```cli
nuget sign <package(s)> [options]
```

in cui `<package(s)>` è uno o più `.nupkg` file.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| CertificateFingerprint | Specifica l'impronta digitale SHA-1 del certificato utilizzato per la ricerca di un archivio certificati locale per il certificato. |
| CertificatePassword | Specifica la password del certificato, se necessario. Se un certificato è protetto da password, ma non viene fornita alcuna password, il comando richiederà una password in fase di esecuzione, a meno che non-opzione interattiva viene passata. |
| CertificatePath | Specifica il percorso del file per il certificato da utilizzare nella firma del pacchetto. |
| CertificateStoreLocation | Specifica il nome dell'utilizzo di archivio certificati X.509 per la ricerca del certificato. Il valore predefinito è "CurrentUser", l'archivio certificati X.509 utilizzato dall'utente corrente. Questa opzione deve essere utilizzata quando si specifica il certificato tramite CertificateSubjectName - o - CertificateFingerprint opzioni. |
| CertificateStoreName | Specifica il nome dell'archivio certificati X.509 da usare per la ricerca del certificato. Il valore predefinito è "My", l'archivio certificati X.509 per i certificati personali. Questa opzione deve essere utilizzata quando si specifica il certificato tramite CertificateSubjectName - o - CertificateFingerprint opzioni. |
| CertificateSubjectName | Specifica il nome del soggetto del certificato utilizzato per la ricerca di un archivio certificati locale per il certificato.  La ricerca è un confronto tra stringhe tra maiuscole e minuscole utilizzando il valore fornito, che verrà trovati tutti i certificati con il nome del soggetto che contiene tale stringa, indipendentemente dagli altri valori dell'oggetto.  L'archivio certificati può essere specificato dalle opzioni CertificateStoreName - e - CertificateStoreLocation. |
| ConfigFile | Il file di configurazione di NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.|
| ForceEnglishOutput | Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese. |
| HashAlgorithm | Algoritmo hash da usare per firmare il pacchetto. Il valore predefinito è SHA256. |
| ? | Visualizza la Guida informazioni per il comando. |
| Non interattive | Elimina richieste di input o conferme dell'utente. |
| OutputDirectory | Specifica la directory in cui salvare il pacchetto firmato. Per impostazione predefinita, il pacchetto originale viene sovrascritto dal pacchetto firmato. |
| Overwrite | Opzione che indica se la firma corrente deve essere sovrascritti. Per impostazione predefinita il comando avrà esito negativo se il pacchetto include già una firma. |
| Timestamper | URL a un server di timestamp RFC 3161. |
| TimestampHashAlgorithm | Algoritmo di hash utilizzabili dal server di timestamp RFC 3161. Il valore predefinito è SHA256. |
| Livello di dettaglio | Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*. |

## <a name="examples"></a>Esempi

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```