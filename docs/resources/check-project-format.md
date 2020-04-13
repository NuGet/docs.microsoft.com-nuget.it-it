---
title: Identificare il formato del progetto
description: Viene descritto come identificare il formato del progetto
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b151547e40e567b38acc2b0b9ee84c50d85000c9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488486"
---
# <a name="identify-the-project-format"></a>Identificare il formato del progetto

NuGet supporta tutti i progetti .NET. Tuttavia, il formato del progetto (di tipo SDK o non in SDK) determina alcuni degli strumenti e dei metodi che è necessario usare per utilizzare e creare pacchetti NuGet. I progetti di tipo SDK usano l'[attributo SDK](/dotnet/core/tools/csproj#additions). È importante identificare il tipo di progetto perché i metodi e gli strumenti usati per utilizzare e creare pacchetti NuGet dipendono dal formato del progetto. Per i progetti non di tipo SDK, i metodi e gli strumenti dipendono anche dal fatto che sia stata eseguita la migrazione del progetto al formato `PackageReference`.

Il fatto che il progetto sia o meno di tipo SDK dipende dal metodo usato per creare il progetto. La tabella seguente mostra il formato di progetto predefinito e lo strumento dell'interfaccia della riga di comando associato per il progetto quando lo si crea con Visual Studio 2017 e versioni successive.

| Progetto&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Formato progetto predefinito | Strumento dell'interfaccia della riga di comando&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Note |
|:------------- |:-------------|:-----|:-----|
| .NET Standard | Stile SDK | [Interfaccia della riga di comando di dotnet](../install-nuget-client-tools.md#dotnetexe-cli) | I progetti creati prima di Visual Studio 2017 non sono di tipo SDK. Usare l'interfaccia della riga di comando `nuget.exe`. |
| .NET Core | Stile SDK | [Interfaccia della riga di comando di dotnet](../install-nuget-client-tools.md#dotnetexe-cli) | I progetti creati prima di Visual Studio 2017 non sono di tipo SDK. Usare l'interfaccia della riga di comando `nuget.exe`. |
| .NET Framework | Non di tipo SDK | [Interfaccia della riga di comando di nuget.exe](../install-nuget-client-tools.md#nugetexe-cli) | I progetti .NET Framework creati con altri metodi possono essere progetti di tipo SDK. Per questi progetti, usare invece l'[interfaccia della riga di comando dotnet](../install-nuget-client-tools.md#dotnetexe-cli). |
| Progetto .NET [migrato](../consume-packages/migrate-packages-config-to-package-reference.md) | Non di tipo SDK| Per creare pacchetti, usare [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration). | Per creare pacchetti, è consigliabile usare `msbuild -t:pack`. Altrimenti, usare l'[interfaccia della riga di comando dotnet](../install-nuget-client-tools.md#dotnetexe-cli). I progetti migrati sono progetti non di tipo SDK. |

## <a name="check-the-project-format"></a>Controllare il formato del progetto

Se non si è certi che il progetto sia di tipo SDK o meno, cercare l'attributo SDK nell'elemento `<Project>` nel file di progetto (per C#, questo è il file con estensione csproj). Se è presente, il progetto è di tipo SDK.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a>Controllare il formato del progetto in Visual Studio

Se si usa Visual Studio, è possibile verificare rapidamente il formato del progetto con uno dei metodi seguenti:

- Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni e scegliere **Modifica nomeprogetto.csproj**.

   Questa opzione è disponibile solo a partire da Visual Studio 2017 per i progetti che usano l'attributo SDK. In caso contrario, usare l'altro metodo.

   ![Modificare il file di progetto](media/edit-project-file.png)

   Un progetto di tipo SDK mostra l'[attributo SDK](/dotnet/core/tools/csproj#additions) nel file di progetto.
   
- Scegliere **Scarica progetto** dal menu **Progetto** oppure fare clic con il pulsante destro del mouse sul progetto e scegliere **Scarica progetto**.

   Questo progetto non includerà l'attributo SDK nel file di progetto. Non è un progetto di tipo SDK.

   ![Scaricare il progetto](media/unload-project.png)

   Fare quindi clic con il pulsante destro del mouse sul progetto scaricato e scegliere **Modifica nomeprogetto.csproj**.

## <a name="see-also"></a>Vedere anche

- [Creare pacchetti .NET Standard con l'interfaccia della riga di comando dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Creare pacchetti .NET Standard con Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [Creare e pubblicare un pacchetto .NET Framework (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [Pack e restore di NuGet come destinazioni MSBuild](../reference/msbuild-targets.md)
