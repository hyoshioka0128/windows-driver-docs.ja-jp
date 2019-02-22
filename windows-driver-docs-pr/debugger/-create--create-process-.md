---
title: に関する (プロセスの作成)
description: に関するコマンドは、新しいターゲット アプリケーションを作成します。
ms.assetid: 9e34eadf-1f68-4eec-ad6b-d70163d5d876
keywords:
- に関する (プロセスを作成する) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .create (Create Process)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a0b03dd9795701910d8d001d6da7f0d9e458a8a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538924"
---
# <a name="create-create-process"></a>に関する (プロセスの作成)


**に関する**コマンドが新しい対象アプリケーションを作成します。

```dbgsyntax
.create [-premote RemoteOptions] [-f] CommandLine 
```

## <a name="span-idddkmetacreateprocessdbgspanspan-idddkmetacreateprocessdbgspanparameters"></a><span id="ddk_meta_create_process_dbg"></span><span id="DDK_META_CREATE_PROCESS_DBG"></span>パラメーター


<span id="_______RemoteOptions______"></span><span id="_______remoteoptions______"></span><span id="_______REMOTEOPTIONS______"></span> *RemoteOptions*   
アタッチする対象のプロセス サーバーを指定します。 オプションは、コマンドラインのものと同じ **-premote**オプション。 参照してください[**スマート クライアントのアクティブ化**](activating-a-smart-client.md)構文の詳細について。

<span id="_______-f______"></span><span id="_______-F______"></span> **-f**   
除くすべてのターゲット アプリケーションのすべてのスレッドを作成する新しいターゲットでフリーズします。 新しく作成されたプロセスで例外が発生するまで、これらのスレッドが固定されます。 最初のブレークポイントが、例外と見なされることに注意してください。 使用して個々 のスレッドを操作できる、 [ **~ (スレッドの固定の解除) u** ](-u--unfreeze-thread-.md)コマンド。

<span id="_______CommandLine______"></span><span id="_______commandline______"></span><span id="_______COMMANDLINE______"></span> *コマンドライン*   
新しいプロセスの完全なコマンドラインを指定します。 *CommandLine*スペースを含めることがあり、引用符で囲む必要がありません。 後のすべてのテキスト、**に関する**コマンドは、の一部として扱われます*CommandLine*; このコマンドのセミコロンや追加のデバッガー コマンドの後にすることはできません。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このコマンドは、CDB が休止状態、または 1 つまたは複数のプロセスのデバッグには、既に場合に使用できます。 WinDbg を休止状態にした場合に使用できません。

デバッガーこのコマンドが成功した場合は、指定されたプロセスが、次回のデバッガー実行コマンドの発行に作成されます。 このコマンドは行で複数回使用する場合は、実行を何度でも、このコマンドの使用として要求する必要があります。

複数のターゲット プロセスは常に実行同時に、いくつかのスレッドの凍結または中断がない限りです。

新しいプロセスを作成し、既存のすべてのターゲットを固定する場合は、-f オプションを使用します。

場合、 **-premote**オプションを使用すると、新しいプロセスは、新しいシステムの一部になります。 詳細については、次を参照してください。[複数のターゲットのデバッグ](debugging-multiple-targets.md)します。

 

 





