---
title: .attach (プロセスにアタッチ)
description: .Attach コマンドは、新しい対象アプリケーションにアタッチします。
ms.assetid: e637c7eb-9c3c-4501-b972-a9293a6da52a
keywords:
- プロセス (.attach) コマンドにアタッチします。
- プロセス (.attach) コマンドをプロセスにアタッチ
- .attach (プロセスにアタッチする) Windows のデバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- .attach (Attach to Process)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ca03126ac57aa6b9a45056e50f2eb7a1cee3f72a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558867"
---
# <a name="attach-attach-to-process"></a>.attach (プロセスにアタッチ)


**.Attach**コマンドが新しい対象アプリケーションにアタッチします。

```dbgcmd    
.attach [-premote RemoteOptions] AttachOptions PID
```

## <a name="span-idddkmetaattachtoprocessdbgspanspan-idddkmetaattachtoprocessdbgspanparameters"></a><span id="ddk_meta_attach_to_process_dbg"></span><span id="DDK_META_ATTACH_TO_PROCESS_DBG"></span>パラメーター


<span id="_______RemoteOptions______"></span><span id="_______remoteoptions______"></span><span id="_______REMOTEOPTIONS______"></span> *RemoteOptions*   
アタッチするプロセス サーバーを指定します。 オプションは、コマンドラインのものと同じ **-premote**オプション。 参照してください[**スマート クライアントのアクティブ化**](activating-a-smart-client.md)構文の詳細について。

<span id="_______AttachOptions______"></span><span id="_______attachoptions______"></span><span id="_______ATTACHOPTIONS______"></span> *AttachOptions*   
アタッチの実行方法を指定します。 これは、次のオプションのいずれかを含めることができます。

<span id="-b"></span><span id="-B"></span>**b**  
デバッガーがターゲット プロセスにアタッチするときに、初期の侵入を要求するを防ぎます。 アプリケーションが既に中断されている場合、またはターゲットに侵入スレッドを作成しないようにする場合は便利にできます。

<span id="-e"></span><span id="-E"></span>**-e**  
により、デバッガーは既にデバッグ中のプロセスにアタッチします。 参照してください[対象アプリケーションを再アタッチ](reattaching-to-the-target-application.md)詳細についてはします。

<span id="-k"></span><span id="-K"></span>**-k**  
ローカルのカーネル デバッグ セッションを開始します。 参照してください[ローカル カーネル デバッグを実行する](performing-local-kernel-debugging.md)詳細についてはします。

<span id="-f"></span><span id="-F"></span>**-f**  
すべてのターゲット アプリケーションのすべてのスレッドを除くにアタッチする新しいターゲットでフリーズします。 新しくアタッチされたプロセスで例外が発生するまで、これらのスレッドが固定されます。 最初のブレークポイントが、例外と見なされることに注意してください。 使用して個々 のスレッドを操作できる、 [ **~ (スレッドの固定の解除) u** ](-u--unfreeze-thread-.md)コマンド。

<span id="-r"></span><span id="-R"></span>**-r**  

原因、デバッガーをアタッチするときに実行されているターゲット プロセスを開始します。 これは、アプリケーションが既に中断されているし、実行を再開する場合に役立ちます。

<span id="-v"></span><span id="-V"></span>**-v**  
指定されたプロセスをもって noninvasively させます。

<span id="_______PID______"></span><span id="_______pid______"></span> *PID*   
新しい対象アプリケーションのプロセス ID を指定します。

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

このコマンドが成功した場合、デバッガーがプロセスにアタッチ、指定した次回デバッガー実行コマンドを発行します。 このコマンドは行で複数回使用する場合は、実行を何度でも、このコマンドの使用として要求する必要があります。

待合室デバッグ中には、実行することはできません、ため、デバッガーは noninvasively、一度に 1 つ以上のプロセスをデバッグすることではありません。 使用しても意味、 **.attach v**コマンドがレンダリング既存侵デバッグ セッションをあまり役に立ちません。

複数のターゲット プロセスは常に実行同時に、いくつかのスレッドの凍結または中断がない限りです。

新しいプロセスにアタッチする、既存のすべてのターゲットを固定は、使用する場合、 **-f**オプション。 たとえば、可能性があります、クライアント アプリケーションでのクラッシュのデバッグありするクライアント アプリケーションを実行できるようにすることがなく、サーバー プロセスにアタッチします。

場合、 **-premote**オプションを使用すると、新しいプロセスは、新しいシステムの一部になります。 詳細については、[複数のターゲットのデバッグ](debugging-multiple-targets.md)を参照してください。

 

 





