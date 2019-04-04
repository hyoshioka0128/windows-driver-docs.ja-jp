---
title: .thread (レジスタ コンテキストの設定)
description: .Thread コマンドでは、どのスレッドに使用されるレジスタのコンテキストを指定します。
ms.assetid: 577276b7-a6c4-427e-ada1-10dbb62ebd5c
keywords:
- 登録のコンテキスト (.thread) コマンドを設定します。
- コンテキストを登録するコンテキストの設定 (.thread) コマンド
- 登録、登録コンテキストの設定 (.thread) コマンド
- 呼び出し履歴を登録するコンテキストの設定 (.thread) コマンド
- .thread (レジスタのコンテキストの設定) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .thread (Set Register Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b5b875b72ad47b4b9c46ff79797518ee3e9b2702
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582164"
---
# <a name="thread-set-register-context"></a>.thread (レジスタ コンテキストの設定)


**.Thread**コマンドでは、スレッドに使用されるレジスタのコンテキストを指定します。

```dbgcmd
.thread [/p [/r] ] [/P] [/w] [Thread]
```

## <a name="span-idddkmetasetregistercontextdbgspanspan-idddkmetasetregistercontextdbgspanparameters"></a><span id="ddk_meta_set_register_context_dbg"></span><span id="DDK_META_SET_REGISTER_CONTEXT_DBG"></span>パラメーター


<span id="________p______"></span><span id="________P______"></span> **/p**   
(ライブ デバッグの場合のみ)このオプションが含まれる場合と*スレッド*が 0 以外の場合、すべて移行ページ テーブル エントリ (Pte) このスレッドを所有しているプロセスを自動的に変換されますにアクセスする前に、物理アドレス。 デバッガーが、このプロセスによって使用されるすべてのメモリの物理アドレスを検索する必要があり、大量のデータは、デバッグ ケーブル間を転送する必要がありますので、パフォーマンス低下があります。 (この動作はいるのと同じ[ **.cache forcedecodeuser**](-cache--set-cache-size-.md))。

場合、 **/p**オプションが含まれると*スレッド*がゼロまたは省略すると、この変換は無効になります。 (この動作はいるのと同じ[ **.cache noforcedecodeuser**](-cache--set-cache-size-.md))。

<span id="________r______"></span><span id="________R______"></span> **/r**   
(ライブ デバッグの場合のみ)場合、 **/r**オプションは、スコープに含める、 **/p**オプション、ユーザー モードのシンボルとレジスタのプロセスのコンテキストを設定した後、このスレッドは再読み込みされますを所有するプロセスをします。 (この動作はいるのと同じ[ **.reload/user**](-reload--reload-module-.md))。

<span id="________P______"></span><span id="________p______"></span> **/P**   
(ライブ デバッグの場合のみ)このオプションが含まれる場合と*スレッド*が 0 以外の場合、すべて移行ページ テーブル エントリ (Pte) は自動的に変換する物理アドレスでアクセスする前にします。 異なり、 **/p**オプション、これにより、すべてのユーザー モードとカーネル モードのプロセスに対して Pte このスレッドを所有しているプロセスだけでなく。 デバッガーが、使用中のすべてのメモリの物理アドレスを検索する必要があり、膨大な量のデータは、デバッグ ケーブル間を転送する必要がありますので、パフォーマンス低下があります。 (この動作はいるのと同じ[ **.cache forcedecodeptes**](-cache--set-cache-size-.md))。

<span id="________w______"></span><span id="________W______"></span> **/w**   
(64 ビットのカーネル デバッグの場合のみ)WOW64 32 ビットのコンテキストには、スレッドのアクティブなコンテキストを変更します。 指定されたスレッドは、WOW64 の状態にあるプロセスで実行する必要があります。

<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
スレッドのアドレス。 これを省略するか、0、スレッド コンテキストは、現在のスレッドにリセットされます。 場合、

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル モードのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

レジスタのコンテキストとその他のコンテキストの設定の詳細については、[変更コンテキスト](changing-contexts.md)を参照してください。

<a name="remarks"></a>コメント
-------

一般に、カーネル デバッグを実行する場合にのみ表示されるレジスタ、現在のスレッドに関連付けられているものです。

**.Thread**コマンドは、レジスタのコンテキストとして指定したスレッドを使用するカーネル デバッガーに指示します。 このコマンドを実行すると、デバッガーは、このスレッドの最も重要なレジスタとスタック トレースへのアクセスがあります。 別のレジスタ コンテキスト コマンドを使用して、またはを実行するターゲットを許可するまで保持されるこのレジスタのコンテキスト (**.thread**、 [ **.cxr**](-cxr--display-context-record-.md)、または[ **.trap**](-trap--display-trap-frame-.md))。 参照してください[登録コンテキスト](changing-contexts.md#register-context)の完全な詳細情報。

**/W**オプションは、64 ビットのカーネル デバッグ WOW64 状態を持つプロセスで実行中のスレッドでのセッションでのみ使用できます。 コンテキストの取得は、WOW64 で記憶最後のコンテキストになりますこれによって実行される最後のユーザー モード コードでは、通常*スレッド*します。 このオプションは、ターゲットがマシンのネイティブ モードの場合にのみ使用できます。 たとえば、ターゲットが x86 ベースのプロセッサの WOW64 の使用をエミュレートしている 64 ビット コンピューターで実行している場合、このオプションは使用できません。 使用して、 **/w**オプションは、x86 ベースのプロセッサに自動的に切り替えるマシン モードになります。

このコマンドは、現在のスレッドを実際に変更されません。 つまりなどの拡張機能[ **! スレッド**](-thread.md)と[ **! teb** ](-teb.md)で引数を使用しない場合、現在のスレッドに既定ではまだします。

次に例を示します。 使用して、 [ **! プロセス**](-process.md)目的のスレッドのアドレスを検索する拡張機能。 (この場合、 **! process 0 0**し、すべてのプロセスを一覧表示するために使用 **! プロセス**を目的のプロセスのすべてのスレッドを一覧表示をもう一度使用します)。

```dbgcmd
kd> !process 0 0
**** NT ACTIVE PROCESS DUMP ****
PROCESS fe5039e0  SessionId: 0  Cid: 0008    Peb: 00000000  ParentCid: 0000
    DirBase: 00030000  ObjectTable: fe529a88  TableSize: 145.
    Image: System

.....

PROCESS ffaa5280  SessionId: 0  Cid: 0120    Peb: 7ffdf000  ParentCid: 01e0
    DirBase: 03b70000  ObjectTable: ffaa4e48  TableSize:  23.
    Image: winmine.exe

kd> !process ffaa5280
PROCESS ffaa5280  SessionId: 0  Cid: 0120    Peb: 7ffdf000  ParentCid: 01e0
    DirBase: 03b70000  ObjectTable: ffaa4e48  TableSize:  23.
    Image: winmine.exe
    VadRoot ffaf6e48 Clone 0 Private 50. Modified 0. Locked 0.
    DeviceMap fe502e88
    Token                             e1b55d70

.....

        THREAD ffaa43a0  Cid 120.3a4  Teb: 7ffde000  Win32Thread: e1b4fea8 WAIT: (WrUserRequest) UserMode Non-Alertable
            ffadc6a0  SynchronizationEvent
        Not impersonating
        Owning Process ffaa5280
        WaitTime (seconds)      24323
        Context Switch Count    494                   LargeStack

.....
```

使用して、 **.thread**目的のスレッドのアドレスを持つコマンド。 これは、レジスタのコンテキストを設定し、重要なレジスタとこのスレッドの呼び出し履歴を調べることができます。

```dbgcmd
kd> .thread ffaa43a0
Using context of thread ffaa43a0

kd> r
Last set context:
eax=00000000 ebx=00000000 ecx=00000000 edx=00000000 esi=00000000 edi=00000000
eip=80403a0d esp=fd581c2c ebp=fd581c60 iopl=0         nv up di pl nz na pe nc
cs=0000  ss=0000  ds=0000  es=0000  fs=0000  gs=0000             efl=00000000
0000:3a0d ??              ???

kd> k
  *** Stack trace for last set context - .thread resets it
ChildEBP RetAddr  
fd581c38 8042d61c ntoskrnl!KiSwapThread+0xc5
00001c60 00000000 ntoskrnl!KeWaitForSingleObject+0x1a1
```

 

 





