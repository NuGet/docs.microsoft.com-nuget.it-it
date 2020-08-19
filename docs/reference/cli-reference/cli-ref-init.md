---
title: Comando init CLI di NuGet
description: Riferimento per il comando nuget.exe init
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3b830d678a473c917b70bd46900bdb0206d3652e
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623084"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="acace-103">comando init (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="acace-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="acace-104">**Si applica a:** versioni supportate per la creazione di pacchetti &bullet; **:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="acace-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="acace-105">Copia tutti i pacchetti da una cartella flat in una cartella di destinazione usando un layout gerarchico come descritto per il [comando Aggiungi](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="acace-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="acace-106">Ovvero, l'utilizzo `init` di equivale a utilizzare il `add` comando su ogni pacchetto nella cartella.</span><span class="sxs-lookup"><span data-stu-id="acace-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="acace-107">Come per `add` , la destinazione deve essere una cartella locale o un percorso UNC; I repository del pacchetto HTTP, ad esempio nuget.org o i server privati, non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="acace-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="acace-108">Uso</span><span class="sxs-lookup"><span data-stu-id="acace-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="acace-109">dove `<source>` è la cartella che contiene i pacchetti e `<destination>` è la cartella locale o il percorso UNC in cui vengono copiati i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="acace-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="acace-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="acace-110">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="acace-111">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="acace-111">The NuGet configuration file to apply.</span></span> <span data-ttu-id="acace-112">Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="acace-112">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="acace-113">Aggiunge tutti i file in ogni pacchetto aggiunto all'origine del pacchetto. uguale `-Expand` a quello del `add` comando.</span><span class="sxs-lookup"><span data-stu-id="acace-113">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="acace-114">*(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="acace-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="acace-115">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="acace-115">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="acace-116">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="acace-116">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="acace-117">Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="acace-117">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="acace-118">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="acace-118">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="acace-119">Esempi</span><span class="sxs-lookup"><span data-stu-id="acace-119">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
