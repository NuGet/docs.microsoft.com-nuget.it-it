---
title: Comando origini CLI NuGet
description: Riferimento per il comando nuget.exe sources
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 73c9cea8200a1ab1937d25a9a611ae7f2a943dba
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622590"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="86374-103">comando Sources (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="86374-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="86374-104">**Si applica a:** utilizzo del pacchetto, pubblicazione delle &bullet; **versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="86374-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="86374-105">Gestisce l'elenco delle origini presenti nel file di configurazione dell'ambito utente o in un file di configurazione specificato.</span><span class="sxs-lookup"><span data-stu-id="86374-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="86374-106">Il file di configurazione dell'ambito utente si trova in `%appdata%\NuGet\NuGet.Config` (Windows) e `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="86374-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="86374-107">Si noti che l'URL di origine di nuget.org è `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="86374-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="86374-108">Uso</span><span class="sxs-lookup"><span data-stu-id="86374-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="86374-109">dove `<operation>` è un *elenco, Aggiungi, Rimuovi, Abilita, Disabilita* o *Aggiorna* `<name>` è il nome dell'origine e `<source>` è l'URL dell'origine.</span><span class="sxs-lookup"><span data-stu-id="86374-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="86374-110">È possibile operare su una sola origine alla volta.</span><span class="sxs-lookup"><span data-stu-id="86374-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="86374-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="86374-111">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="86374-112">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="86374-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="86374-113">Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="86374-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="86374-114">*(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="86374-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Format`**

  <span data-ttu-id="86374-115">Si applica all' `list` azione e può essere `Detailed` (impostazione predefinita) o `Short` .</span><span class="sxs-lookup"><span data-stu-id="86374-115">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span>

- **`-?|-help`**

  <span data-ttu-id="86374-116">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="86374-116">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="86374-117">Nome dell'origine.</span><span class="sxs-lookup"><span data-stu-id="86374-117">Name of the source.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="86374-118">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="86374-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Password`**

  <span data-ttu-id="86374-119">Specifica la password per l'autenticazione con l'origine.</span><span class="sxs-lookup"><span data-stu-id="86374-119">Specifies the password for authenticating with the source.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="86374-120">Percorso dell'origine dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="86374-120">Path to the package(s) source.</span></span>

- **`-StorePasswordInClearText`**

  <span data-ttu-id="86374-121">Indica per archiviare la password in testo non crittografato anziché il comportamento predefinito di archiviazione di un modulo crittografato.</span><span class="sxs-lookup"><span data-stu-id="86374-121">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span>

- **`-UserName`**

  <span data-ttu-id="86374-122">Specifica il nome utente per l'autenticazione con l'origine.</span><span class="sxs-lookup"><span data-stu-id="86374-122">Specifies the user name for authenticating with the source.</span></span>

- **`-ValidAuthenticationTypes`**

  <span data-ttu-id="86374-123">Elenco delimitato da virgole di tipi di autenticazione validi per questa origine.</span><span class="sxs-lookup"><span data-stu-id="86374-123">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="86374-124">Per impostazione predefinita, tutti i tipi di autenticazione sono validi.</span><span class="sxs-lookup"><span data-stu-id="86374-124">By default, all authentication types are valid.</span></span> <span data-ttu-id="86374-125">Esempio: `basic,negotiate`.</span><span class="sxs-lookup"><span data-stu-id="86374-125">Example: `basic,negotiate`.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="86374-126">Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="86374-126">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

> [!Note]
> <span data-ttu-id="86374-127">Assicurarsi di aggiungere la password delle origini nello stesso contesto utente in cui il nuget.exe viene usato in un secondo momento per accedere all'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="86374-127">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="86374-128">La password verrà archiviata crittografata nel file di configurazione e potrà essere decrittografata solo nello stesso contesto utente in cui è stata crittografata.</span><span class="sxs-lookup"><span data-stu-id="86374-128">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="86374-129">Quindi, ad esempio, quando si usa un server di compilazione per ripristinare i pacchetti NuGet, la password deve essere crittografata con lo stesso utente di Windows in cui verrà eseguita l'attività del server di compilazione.</span><span class="sxs-lookup"><span data-stu-id="86374-129">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="86374-130">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="86374-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="86374-131">Esempi</span><span class="sxs-lookup"><span data-stu-id="86374-131">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
