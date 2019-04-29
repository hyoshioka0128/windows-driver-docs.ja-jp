---
title: .context (ユーザーモード アドレス コンテキストの設定)
description: .Context コマンドでは、ユーザー モード アドレスのコンテキストで使用するプロセスのどのページのディレクトリを指定または、現在のユーザー モード アドレス コンテキストが表示されます。
ms.assetid: f859b9bf-c05a-44cd-b6f0-8ff4561ddd4e
keywords:
- ユーザー モード アドレス コンテキスト (.context) コマンドを設定します。
- アドレス、ユーザー モード アドレス コンテキストの設定 (.context) コマンド
- コンテキスト、ユーザー モード アドレス コンテキストの設定 (.context) コマンド
- .context (ユーザー モード アドレス コンテキストの設定) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .context (Set User-Mode Address Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 14b6d270f3a75516c1732da48f16b30728c60701
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334621"
---
# <a name="context-set-user-mode-address-context"></a>.context (ユーザーモード アドレス コンテキストの設定)


**.Context**コマンドがユーザー モード アドレスのコンテキストで使用するプロセスのどのページのディレクトリを指定または現在のユーザー モード アドレス コンテキストが表示されます。

```dbgsyntax
.context [PageDirectoryBase]
```

## <a name="span-idddkmetasetusermodeaddresscontextdbgspanspan-idddkmetasetusermodeaddresscontextdbgspanparameters"></a><span id="ddk_meta_set_user_mode_address_context_dbg"></span><span id="DDK_META_SET_USER_MODE_ADDRESS_CONTEXT_DBG"></span>パラメーター


<span id="_______PageDirectoryBase______"></span><span id="_______pagedirectorybase______"></span><span id="_______PAGEDIRECTORYBASE______"></span> *PageDirectoryBase*   
必要なプロセスのページのディレクトリのベース アドレスを指定します。 ユーザー モード アドレス コンテキストは、このページのディレクトリに設定されます。 場合*PageDirectoryBase* 0 の場合は、ユーザー モード アドレス コンテキストは現在のシステム状態のページのディレクトリに設定されます。 場合*PageDirectoryBase*は省略すると、現在のユーザー モード アドレス コンテキストが表示されます。

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

ユーザー モード アドレス コンテキストとその他のコンテキストの設定の詳細については、次を参照してください。[変更コンテキスト](changing-contexts.md)します。

<a name="remarks"></a>コメント
-------

通常、カーネル デバッグを実行している場合にのみ表示されるユーザー モード アドレス空間には、現在のプロセスに関連付けられている 1 つです。

**.Context**コマンドとして指定したページのディレクトリを使用する、カーネル デバッガーに指示、*ユーザー モード アドレス コンテキスト*します。 このコマンドが実行された後、デバッガーは仮想アドレス空間にアクセスがあります。 このアドレス空間のページ テーブルは、すべてのユーザー モードのメモリ アドレスの解釈に使用されます。 これにより、このメモリを読み書きすることができます。

[ **.Process (プロセス コンテキストの設定)** ](-process--set-process-context-.md)コマンドには、同様の効果。 ただし、 **.context**コマンドは、特定のページのディレクトリにユーザー モード アドレス コンテキストを設定中に、 **.process**コマンドのセット、*プロセス コンテキスト*特定するプロセスです。 X86 プロセッサでは、これら 2 つのコマンドが基本的に同じ効果があります。 ただし、Itanium プロセッサが 1 つのプロセスは、ページの 1 つ以上のディレクトリがあります。 ここで、 **.process**プロセスに関連付けられているすべてのページのディレクトリにアクセスできるようになりますので、コマンドより強力なは。 参照してください[プロセス コンテキスト](changing-contexts.md#process-context)の詳細。

発行する必要がありますライブ デバッグを実行する場合、 [ **.cache forcedecodeuser** ](-cache--set-cache-size-.md)コマンドに加え、 **.context**コマンド。 これにより、必要なメモリ領域の物理アドレスを検索するデバッガーが強制されます。 (この遅くなること、ため、多くの場合、デバッグ ケーブル間、膨大な量のデータを転送する必要があります。)

クラッシュ ダンプのデバッグを実行している場合、 [ **.cache** ](-cache--set-cache-size-.md)コマンドは必要ありません。 ただし、ことはできません、仮想アドレス空間の任意の部分へのアクセスの場合にディスクにページングされたユーザー モード プロセスのクラッシュが発生しました。

次に例を示します。 使用して、 [ **! プロセス**](-process.md)目的のプロセスの基本ディレクトリを検索する拡張機能。

```dbgcmd
kd> !process 0 0
**** NT ACTIVE PROCESS DUMP ****
PROCESS fe5039e0  SessionId: 0  Cid: 0008    Peb: 00000000  ParentCid: 0000
    DirBase: 00030000  ObjectTable: fe529b68  TableSize:  50.
    Image: System

...

PROCESS fe3c0d60  SessionId: 0  Cid: 0208    Peb: 7ffdf000  ParentCid: 00d4
 DirBase: 0011f000  ObjectTable: fe3d0f48  TableSize:  30.
    Image: regsvc.exe
```

使用して、 **.context**コマンドには、このページのディレクトリ ベース。

```dbgcmd
kd> .context 0011f000
```

これにより、さまざまな方法でアドレス空間を確認できます。 たとえばの出力をここでは、 [ **! peb** ](-peb.md)拡張機能。

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

 

 





