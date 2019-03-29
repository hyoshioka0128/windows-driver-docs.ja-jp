---
title: .process (プロセス コンテキストの設定)
description: .Process コマンドでは、どのプロセスがプロセスのコンテキストの使用を指定します。
ms.assetid: f454faef-bc28-43f1-b511-bcee0c12fc24
keywords:
- 設定するプロセスのコンテキスト (.process) コマンド
- アドレス、プロセスのコンテキストを設定する (.process) コマンド
- コンテキスト、プロセスのコンテキストを設定する (.process) コマンド
- プロセスのプロセスのコンテキストを設定する (.process) コマンド
- .process (プロセス コンテキストの設定) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .process (Set Process Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3ad91066a0d80f68a64ee2fe213e30bbda8acea4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582515"
---
# <a name="process-set-process-context"></a>.process (プロセス コンテキストの設定)


**.Process**コマンドでは、どのプロセスがプロセスのコンテキストの使用を指定します。

```dbgcmd
.process [/i] [/p [/r]] [/P] [Process]
```

## <a name="span-idddkmetasetprocesscontextdbgspanspan-idddkmetasetprocesscontextdbgspanparameters"></a><span id="ddk_meta_set_process_context_dbg"></span><span id="DDK_META_SET_PROCESS_CONTEXT_DBG"></span>パラメーター


<span id="________i______"></span><span id="________I______"></span> **/i**   
ライブ デバッグだけです。ローカル カーネル デバッグ) 中にないことを指定します。*プロセス*をデバッグする*invasively*します。 この種のデバッグを意味する対象のコンピューターのオペレーティング システム実際には、指定されたプロセス active。 (このオプションを指定せず、 **.process**コマンドは、デバッガーの出力を変更しますが、ターゲット コンピューター自体には影響しません)。使用する場合 **/i**、使用する必要があります、 [ **g (移動)** ](g--go-.md)ターゲットを実行するコマンド。 数秒後、ターゲット改行に戻りを使用して、デバッガーの指定した*プロセス*がアクティブで、プロセスのコンテキストで使用されます。

<span id="________p______"></span><span id="________P______"></span> **/p**   
使用する場合、アクセスする前に、物理アドレスには、このプロセスのすべての遷移のページ テーブル エントリ (Pte) を変換 **/p**と*プロセス*が 0 以外。 この変換では、デバッガーは、このプロセスで使用されるメモリのすべての物理アドレスを見つける必要がありますので、パフォーマンス低下、なることがあります。 また、デバッガーはデバッグ ケーブルの間で大量のデータを転送する必要があります。 (この動作は同じ[ **.cache forcedecodeuser**](-cache--set-cache-size-.md))。

含める場合は、 **/p**オプションと*プロセス*がゼロまたは省略すると、変換が無効になっています。 (この動作は同じ[ **.cache noforcedecodeptes**](-cache--set-cache-size-.md))。

<span id="________r______"></span><span id="________R______"></span> **/r**   
使用する場合、プロセスのコンテキストを設定した後にユーザー モードのシンボルを再読み込み、 **/r**と **/p**オプション。 (この動作は同じ[ **.reload/user**](-reload--reload-module-.md))。

<span id="________P______"></span><span id="________p______"></span> **/P**   
(ライブ デバッグおよび完全メモリ ダンプのみ)使用する場合は、すべて移行ページ テーブル エントリ (Pte) にアクセスする前に、物理アドレスを変換 **/P**と*プロセス*が 0 以外。 異なり、 **/p**オプション、 **/P**オプションがすべてのユーザー モードとカーネル モード プロセスを指定されたプロセスだけでなく Pte を変換します。 この変換では、デバッガーが使用されているすべてのメモリの物理アドレスを見つける必要がありますので、パフォーマンス低下、なることがあります。 また、デバッガーはデバッグ ケーブルの間で大量のデータを転送する必要があります。 (この動作は同じ[ **.cache forcedecodeptes**](-cache--set-cache-size-.md))。

<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span> *プロセス*   
使用するプロセスのアドレスを指定します。 (正確には、このパラメーターはこのプロセスの」プロセス ブロックのアドレスを指定します)。 プロセスのコンテキストは、このプロセスに設定されます。 省略した場合*プロセス*0 を指定またはプロセスのコンテキストが現在のシステム状態の既定のプロセスにリセットされます。 (を使用した場合、 **/i**プロセスのコンテキストを設定するオプションは、使用する必要があります、 **/i**プロセスのコンテキストをリセットするにはオプションです)。

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
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

プロセスのコンテキストとその他のコンテキストの設定の詳細については、次を参照してください。[変更コンテキスト](changing-contexts.md)します。

<a name="remarks"></a>コメント
-------

通常、カーネル デバッグを実行している場合にのみ表示されるユーザー モード アドレス空間には、現在のプロセスに関連付けられている 1 つは。

**.Process**コマンドとして特定のユーザー モード プロセスを使用してカーネル デバッガーに指示、*プロセス コンテキスト*します。 この使用状況がいくつかの効果がデバッガーでこのプロセスの仮想アドレス空間へのアクセスがある最も重要です。 デバッガーでは、このプロセスのページ テーブルを使用して、このメモリへの書き込みし、読み取りできるように、すべてのユーザー モード メモリ アドレスを解釈します。

[ **.Context (ユーザー モード アドレス コンテキストの設定)** ](-context--set-user-mode-address-context-.md)コマンドには、同様の効果。 ただし、 **.context**コマンドのセット、*ユーザー モード アドレス コンテキスト*に特定のページのディレクトリでは、中に、 **.process**コマンドを特定のプロセスのコンテキストの設定プロセスです。 X86 ベースのプロセッサで **.context**と **.process**ほぼ同じ効果があります。 ただし、Itanium ベースのプロセッサでは、1 つのプロセスは、ページの 1 つ以上のディレクトリがあります。 このような状況で、 **.process**コマンドは、すべてのプロセスに関連付けられているページのディレクトリにアクセスできるため、さらに強力です。 プロセスのコンテキストの詳細については、次を参照してください。[プロセス コンテキスト](changing-contexts.md#process-context)します。

**注**  ライブ デバッグを実行する場合は使用、 **/i**または **/p**パラメーター。 これらのパラメーターのないユーザー モードまたはセッションのメモリを正しく表示できません。

 

**/I**パラメーターには、ターゲット プロセスがアクティブにします。 このオプションを使用する場合、ターゲットを有効にするには、このコマンドに対して 1 回を実行する必要があります。 もう一度実行すると、プロセスのコンテキストが失われます。

**/P**パラメーターを使用する、 **forcedecodeuser**設定します。 (を使用する必要はありません **/p**場合、 **forcedecodeuser**オプションが既にアクティブです)。プロセスのコンテキストと**forcedecodeuser**状態のまま、ターゲットをもう一度実行までの間だけです。

クラッシュ ダンプのデバッグを実行している場合、 **/i**と **/p**オプションは使用できません。 任意の部分にアクセスすることはできませんただし、ディスクにページングされたユーザー モード プロセスの仮想アドレス空間のクラッシュが発生しました。

カーネル デバッガーを使用して、ユーザーの領域にブレークポイントを設定、使用する場合、 **/i**にターゲットを適切なプロセスのコンテキストに切り替えるオプション。

次の例は、使用する方法を示します、 [ **! プロセス**](-process.md) 」プロセス ブロックのアドレスを目的のプロセスを検索する拡張機能。

```dbgcmd
kd> !process 0 0
**** NT ACTIVE PROCESS DUMP ****
PROCESS fe5039e0  SessionId: 0  Cid: 0008    Peb: 00000000  ParentCid: 0000
    DirBase: 00030000  ObjectTable: fe529b68  TableSize:  50.
    Image: System

.....

PROCESS fe3c0d60  SessionId: 0  Cid: 0208    Peb: 7ffdf000  ParentCid: 00d4
    DirBase: 0011f000  ObjectTable: fe3d0f48  TableSize:  30.
    Image: regsvc.exe
```

この例ではこれで、 **.process**コマンドには、このプロセスのアドレス。

```dbgcmd
kd> .process fe3c0d60
Implicit process is now fe3c0d60
```

このコマンドは、通知、 [ **.context** ](-context--set-user-mode-address-context-.md)コマンドは不要です。 ユーザー モード アドレス コンテキストは、目的の値を既に持っています。

```dbgcmd
kd> .context 
User-mode page directory base is 11f000
```

この値では、さまざまな方法でアドレス空間を確認することができます。 たとえば、次の例には、出力は示しています。、 [ **! peb** ](-peb.md)拡張機能。

```dbgcmd
kd> !peb
PEB at 7FFDF000
    InheritedAddressSpace:    No
    ReadImageFileExecOptions: No
    BeingDebugged:            No
    ImageBaseAddress:         01000000
    Ldr.Initialized: Yes
    Ldr.InInitializationOrderModuleList: 71f40 . 77f68
    Ldr.InLoadOrderModuleList: 71ec0 . 77f58
    Ldr.InMemoryOrderModuleList: 71ec8 . 77f60
        01000000 C:\WINNT\system32\regsvc.exe
        77F80000 C:\WINNT\System32\ntdll.dll
        77DB0000 C:\WINNT\system32\ADVAPI32.dll
        77E80000 C:\WINNT\system32\KERNEL32.DLL
        77D40000 C:\WINNT\system32\RPCRT4.DLL
        77BE0000 C:\WINNT\system32\secur32.dll
    SubSystemData:     0
    ProcessHeap:       70000
    ProcessParameters: 20000
        WindowTitle:  'C:\WINNT\system32\regsvc.exe'
        ImageFile:    'C:\WINNT\system32\regsvc.exe'
        CommandLine:  'C:\WINNT\system32\regsvc.exe'
        DllPath:     'C:\WINNT\system32;.;C:\WINNT\System32;C:\WINNT\system;C:\WINNT;C:\WINNT\system32;C:\WINNT;C:\WINNT\System32\Wbem;C:\PROGRA~1\COMMON~1\AUTODE~1'
        Environment:  0x10000
```

 

 





