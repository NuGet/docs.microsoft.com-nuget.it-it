---
title: NuGet CLI origini comando | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Riferimento per il nuget.exe origini comando
keywords: NuGet origini di riferimento, le origini di comando
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f682a5209556ec6741473ccf2648e8f38bb568b9
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="577e0-104">comando origini (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="577e0-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="577e0-105">**Si applica a:** il consumo di pacchetti, pubblicazione &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="577e0-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="577e0-106">Gestisce l'elenco delle origini nel file di configurazione di ambito di utente o un file di configurazione specificato.</span><span class="sxs-lookup"><span data-stu-id="577e0-106">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="577e0-107">Il file di configurazione di ambito di utente si trova in `%appdata%\NuGet\NuGet.Config` (Windows) e `~/.nuget/NuGet/NuGet.Config` (Mac o Linux).</span><span class="sxs-lookup"><span data-stu-id="577e0-107">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="577e0-108">Si noti che l'URL di origine di nuget.org è `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="577e0-108">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="577e0-109">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="577e0-109">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="577e0-110">dove `<operation>` è uno dei *elenco, aggiungere, rimuovere, attivare, disattivare* o *aggiornamento*, `<name>` è il nome dell'origine, e `<source>` è l'URL dell'origine.</span><span class="sxs-lookup"><span data-stu-id="577e0-110">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="577e0-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="577e0-111">Options</span></span>

| <span data-ttu-id="577e0-112">Opzione</span><span class="sxs-lookup"><span data-stu-id="577e0-112">Option</span></span> | <span data-ttu-id="577e0-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="577e0-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="577e0-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="577e0-114">ConfigFile</span></span> | <span data-ttu-id="577e0-115">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="577e0-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="577e0-116">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="577e0-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="577e0-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="577e0-117">ForceEnglishOutput</span></span> | <span data-ttu-id="577e0-118">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="577e0-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="577e0-119">Formato</span><span class="sxs-lookup"><span data-stu-id="577e0-119">Format</span></span> | <span data-ttu-id="577e0-120">Si applica al `list` azione e può essere `Detailed` (impostazione predefinita) o `Short`.</span><span class="sxs-lookup"><span data-stu-id="577e0-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="577e0-121">?</span><span class="sxs-lookup"><span data-stu-id="577e0-121">Help</span></span> | <span data-ttu-id="577e0-122">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="577e0-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="577e0-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="577e0-123">NonInteractive</span></span> | <span data-ttu-id="577e0-124">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="577e0-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="577e0-125">Password</span><span class="sxs-lookup"><span data-stu-id="577e0-125">Password</span></span> | <span data-ttu-id="577e0-126">Specifica la password per l'autenticazione con l'origine.</span><span class="sxs-lookup"><span data-stu-id="577e0-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="577e0-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="577e0-127">StorePasswordInClearText</span></span> | <span data-ttu-id="577e0-128">Indica di archiviare la password in testo non crittografato anziché il comportamento predefinito di archiviazione di un formato crittografato.</span><span class="sxs-lookup"><span data-stu-id="577e0-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="577e0-129">UserName</span><span class="sxs-lookup"><span data-stu-id="577e0-129">UserName</span></span> | <span data-ttu-id="577e0-130">Specifica il nome utente per l'autenticazione con l'origine.</span><span class="sxs-lookup"><span data-stu-id="577e0-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="577e0-131">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="577e0-131">Verbosity</span></span> | <span data-ttu-id="577e0-132">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="577e0-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="577e0-133">Assicurarsi di aggiungere password delle origini nel contesto dell'utente stesso come il nuget.exe viene successivamente utilizzato per accedere all'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="577e0-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="577e0-134">La password verrà archiviata crittografati nel file di configurazione e può essere decrittografata solo nello stesso contesto utente come è stato crittografato.</span><span class="sxs-lookup"><span data-stu-id="577e0-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="577e0-135">Ad esempio quando si utilizza un server di compilazione per il ripristino dei pacchetti NuGet che la password deve essere crittografata con lo stesso utente di Windows in cui verrà eseguita l'attività del server di compilazione.</span><span class="sxs-lookup"><span data-stu-id="577e0-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="577e0-136">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="577e0-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="577e0-137">Esempi</span><span class="sxs-lookup"><span data-stu-id="577e0-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
