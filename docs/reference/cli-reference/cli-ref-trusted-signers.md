---
title: Comando per i firmatari dell'interfaccia della riga di comando di NuGet
description: Riferimento per il comando nuget.exe Trusted-signers
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 2753f92601b3d8b43593762cc07cd8384646feea
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622668"
---
# <a name="trusted-signers-command-nuget-cli"></a>comando Trusted-signers (interfaccia della riga di comando di NuGet)

**Si applica a:** versioni supportate per l'utilizzo di pacchetti &bullet; **:** 4.9.1 +

Ottiene o imposta i firmatari attendibili per la configurazione NuGet. Per ulteriori informazioni sull'utilizzo, vedere [configurazioni comuni di NuGet](../../consume-packages/configuring-nuget-behavior.md). Per informazioni dettagliate sull'aspetto dello schema di nuget.config, vedere il [riferimento al file di configurazione NuGet](../nuget-config-file.md).

## <a name="usage"></a>Uso

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Se non `list|add|remove|sync` viene specificato alcun parametro, il comando utilizzerà per impostazione predefinita `list` .

## <a name="nuget-trusted-signers-list"></a>elenco di firmatari attendibili NuGet

Elenca tutti i firmatari attendibili nella configurazione. Questa opzione includerà tutti i certificati (con algoritmo di impronta digitale e impronta digitale) di ogni firmatario. Se un certificato ha un precedente `[U]` , significa che la voce del certificato è `allowUntrustedRoot` impostata come `true` .

Di seguito è riportato un esempio di output di questo comando:

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>NuGet Trusted-signers Add [opzioni]

Aggiunge al file di configurazione un firmatario attendibile con il nome specificato. Questa opzione ha movimenti diversi per aggiungere un autore o un repository attendibile.

## <a name="options-for-add-based-on-a-package"></a>Opzioni per l'aggiunta in base a un pacchetto

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

dove `<package(s)>` è uno o più `.nupkg` file.

- **`-Author`**

  Specifica che la firma dell'autore dei pacchetti deve essere attendibile.

- **`-AllowUntrustedRoot`**

  Specifica se il certificato per il firmatario attendibile deve essere concatenato a una radice non attendibile.

- **`-Owners`**

  Elenco separato da punto e virgola di proprietari attendibili per limitare ulteriormente la relazione di trust di un repository. Valido solo quando si usa l' `-Repository` opzione.

- **`-Repository`**

  Specifica che la firma del repository o il controfirma dei pacchetti deve essere attendibile.

`-Author` `-Repository` Non è supportata la specifica di e allo stesso tempo.

## <a name="options-for-add-based-on-a-service-index"></a>Opzioni per l'aggiunta in base a un indice del servizio

```cli
nuget trusted-signers add -Name <name> [options]
```

_Nota_: questa opzione consente di aggiungere solo repository attendibili. 

- **`-AllowUntrustedRoot`**

  Specifica se il certificato per il firmatario attendibile deve essere concatenato a una radice non attendibile.

- **`-Owners`**

  Elenco separato da punto e virgola di proprietari attendibili per limitare ulteriormente la relazione di trust di un repository.

- **`-ServiceIndex`**

  Specifica l'indice del servizio V3 del repository da ritenere attendibile. Questo repository deve supportare la risorsa delle firme del repository. Se non viene specificato, il comando cercherà un'origine del pacchetto con lo stesso `-Name` e otterrà l'indice del servizio.

## <a name="options-for-add-based-on-the-certificate-information"></a>Opzioni per l'aggiunta in base alle informazioni sul certificato

```cli
nuget trusted-signers add -Name <name> [options]
```

_Nota_: se un firmatario attendibile con il nome specificato esiste già, l'elemento del certificato verrà aggiunto a tale firmatario. In caso contrario, verrà creato un autore attendibile con un elemento certificato fornito dalle informazioni del certificato.


- **`-AllowUntrustedRoot`**

  Specifica se il certificato per il firmatario attendibile deve essere concatenato a una radice non attendibile.

- **`-CertificateFingerprint`**

  Specifica le impronte digitali di un certificato con cui devono essere firmati i pacchetti firmati. Un'impronta digitale del certificato è un hash del certificato. L'algoritmo hash usato per il calcolo di questo hash deve essere specificato nell' `FingerprintAlgorithm` opzione.

- **`-FingerprintAlgorithm`**

  Specifica l'algoritmo hash usato per calcolare l'impronta digitale del certificato. Il valore predefinito è `SHA256`. I valori supportati sono `SHA256` , `SHA384` e `SHA512` .

## <a name="nuget-trusted-signers-remove--name-name"></a>Nome attendibile-signers di NuGet \<name\>

Rimuove eventuali firmatari attendibili che corrispondono al nome specificato.

## <a name="nuget-trusted-signers-sync--name-name"></a>Nome-sincronizzazione di NuGet Trusted-signers \<name\>

Richiede l'elenco più recente di certificati usati in un repository attualmente attendibile per aggiornare l'elenco di certificati esistente nel firmatario attendibile.

_Nota_: questo movimento eliminerà l'elenco corrente dei certificati e li sostituirà con un elenco aggiornato dal repository.

## <a name="options"></a>Opzioni

- **`-ConfigFile`**

  File di configurazione NuGet da applicare. Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.

- **`-?|-help`**

  Visualizza le informazioni della Guida per il comando.

- **`-Name`**

  Nome del firmatario attendibile.

- **`-NonInteractive`**

  Evita la richiesta di input o conferme dell'utente.

- **`-Verbosity [normal|quiet|detailed]`**

  Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .


## <a name="examples"></a>Esempi

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
