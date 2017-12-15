---
title: NuGet CLI origini comando | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 997ce736-91ba-4cd2-88c9-b4b168e3130a
description: Riferimento per il nuget.exe origini comando
keywords: NuGet origini di riferimento, le origini di comando
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 52c46dba168e7395d50cb8d8f9775839389e614c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="97dd2-104">comando origini (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="97dd2-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="97dd2-105">**Si applica a:** il consumo di pacchetti, pubblicazione &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="97dd2-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="97dd2-106">Gestisce l'elenco delle origini nel `%AppData%\NuGet\NuGet.Config` o file di configurazione specificato.</span><span class="sxs-lookup"><span data-stu-id="97dd2-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

## <a name="usage"></a><span data-ttu-id="97dd2-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="97dd2-107">Usage</span></span>

```
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="97dd2-108">dove `<operation>` è uno dei *elenco, aggiungere, rimuovere, attivare, disattivare* o *aggiornamento*, `<name>` è il nome dell'origine, e `<source>` è l'URL dell'origine.</span><span class="sxs-lookup"><span data-stu-id="97dd2-108">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>


## <a name="options"></a><span data-ttu-id="97dd2-109">Opzioni</span><span class="sxs-lookup"><span data-stu-id="97dd2-109">Options</span></span>

| <span data-ttu-id="97dd2-110">Opzione</span><span class="sxs-lookup"><span data-stu-id="97dd2-110">Option</span></span> | <span data-ttu-id="97dd2-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="97dd2-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="97dd2-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="97dd2-112">ConfigFile</span></span> | <span data-ttu-id="97dd2-113">*(2.5 +)*  Questo file di configurazione da applicare.</span><span class="sxs-lookup"><span data-stu-id="97dd2-113">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="97dd2-114">Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="97dd2-114">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="97dd2-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="97dd2-115">ForceEnglishOutput</span></span> | <span data-ttu-id="97dd2-116">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="97dd2-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="97dd2-117">Formato</span><span class="sxs-lookup"><span data-stu-id="97dd2-117">Format</span></span> | <span data-ttu-id="97dd2-118">Si applica al `list` azione e può essere `Detailed` (impostazione predefinita) o `Short`.</span><span class="sxs-lookup"><span data-stu-id="97dd2-118">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="97dd2-119">?</span><span class="sxs-lookup"><span data-stu-id="97dd2-119">Help</span></span> | <span data-ttu-id="97dd2-120">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="97dd2-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="97dd2-121">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="97dd2-121">NonInteractive</span></span> | <span data-ttu-id="97dd2-122">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="97dd2-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="97dd2-123">Password</span><span class="sxs-lookup"><span data-stu-id="97dd2-123">Password</span></span> | <span data-ttu-id="97dd2-124">Specifica la password per l'autenticazione con l'origine.</span><span class="sxs-lookup"><span data-stu-id="97dd2-124">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="97dd2-125">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="97dd2-125">StorePasswordInClearText</span></span> | <span data-ttu-id="97dd2-126">Indica di archiviare la password in testo non crittografato anziché il comportamento predefinito di archiviazione di un formato crittografato.</span><span class="sxs-lookup"><span data-stu-id="97dd2-126">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="97dd2-127">UserName</span><span class="sxs-lookup"><span data-stu-id="97dd2-127">UserName</span></span> | <span data-ttu-id="97dd2-128">Specifica il nome utente per l'autenticazione con l'origine.</span><span class="sxs-lookup"><span data-stu-id="97dd2-128">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="97dd2-129">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="97dd2-129">Verbosity</span></span> | <span data-ttu-id="97dd2-130">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="97dd2-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

> [!Note]
> <span data-ttu-id="97dd2-131">Assicurarsi di aggiungere password delle origini nel contesto dell'utente stesso come il nuget.exe viene successivamente utilizzato per accedere all'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="97dd2-131">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="97dd2-132">La password verrà archiviata crittografati nel file di configurazione e può essere decrittografata solo nello stesso contesto utente come è stato crittografato.</span><span class="sxs-lookup"><span data-stu-id="97dd2-132">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="97dd2-133">Ad esempio quando si utilizza un server di compilazione per il ripristino dei pacchetti NuGet che la password deve essere crittografata con lo stesso utente di Windows in cui verrà eseguita l'attività del server di compilazione.</span><span class="sxs-lookup"><span data-stu-id="97dd2-133">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="97dd2-134">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="97dd2-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="97dd2-135">Esempi</span><span class="sxs-lookup"><span data-stu-id="97dd2-135">Examples</span></span>

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
