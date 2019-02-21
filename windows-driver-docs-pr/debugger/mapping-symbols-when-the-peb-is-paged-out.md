---
title: ページ アウトは、シンボルと、PEB のマッピング
description: ページ アウトは、シンボルと、PEB のマッピング
ms.assetid: dba9e686-81fc-4efa-a5c7-293b9e47e0b1
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 720e77a91266fb7589bbaaf383c1b6fd6c361607
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536652"
---
# <a name="mapping-symbols-when-the-peb-is-paged-out"></a>ページ アウトは、シンボルと、PEB のマッピング


## <span id="ddk_invalid_or_missing_symbols_dbg"></span><span id="DDK_INVALID_OR_MISSING_SYMBOLS_DBG"></span>


シンボルを読み込むには、デバッガーは、オペレーティング システムによって読み込まれたモジュールの一覧を検索します。 ユーザー モードのモジュールの一覧へのポインターでは、プロセスの環境ブロック (PEB) に格納された項目の 1 つです。

メモリを解放するには、メモリ マネージャーは、領域の他のプロセスまたはカーネル モードのコンポーネントをユーザー モードのデータをページ可能性があります。 ユーザー モードのデータがページ アウトいる PEB データ構造体を含めることができます。 このデータ構造がなければ、デバッガーが、どのイメージを読み込むシンボルを判断できません。

**注**  ユーザー モードのモジュールに対してのみのシンボル ファイルに影響します。 カーネル モードのモジュールとシンボルは影響しません、ように別のリストで追跡されます。

 

ユーザー モードのモジュールが現在のプロセスにマップされているし、その記号を修正したいとします。 モジュールの仮想アドレスの範囲で任意のアドレスを検索します。 たとえば、モジュールがアドレス 7f78e9e000F を含む仮想アドレスの範囲にマップされているとします。 次のコマンドを入力します。

```dbgcmd
3: kd> !vad 7f78e9e000F 1
```

コマンドの出力には、モジュールの仮想アドレス記述子 (VAD) に関する情報が表示されます。 コマンドの出力には、モジュールのシンボルを読み込むために使用できる、再読み込みコマンド文字列も含まれています。 開始アドレスが再読み込みコマンド文字列に含まれています (000007f7\`8e9e0000) と、メモ帳モジュールのサイズ (32000)。

```dbgcmd
VAD @ fffffa80056fb960
...
Reload command: .reload notepad.exe=000007f7`8e9e0000,32000
```

シンボルを読み込むには、再読み込みコマンド文字列で指定されたコマンドを入力します。

```dbgcmd
.reload notepad.exe=000007f7`8e9e0000,32000
```

若干異なる手法を使用する別の例を次に示します。 使用する方法を示します、 [ **! vad** ](-vad.md) PEB にページ アウトされたときに、シンボルをマップする拡張機能。基本的な考え方は、開始アドレスと関連する DLL のサイズを検索し、使用することができるようにする、 [ **.reload** ](-reload--reload-module-.md)のために必要なシンボルを読み込むコマンド。 現在のプロセスのアドレスが 0xE0000126 であると仮定\`01BA0AF0 する記号を修正します。 まず、使用して、 [ **! プロセス**](-process.md)仮想アドレス記述子 (VAD) のルートのアドレスを取得するコマンド。

```dbgcmd
kd> !process e000012601ba0af0 1
PROCESS e000012601ba0af0
    SessionId: 2  Cid: 0b50    Peb: 6fbfffde000  ParentCid: 0efc
    DirBase: 079e8461  ObjectTable: e000000600fbceb0  HandleCount: 360.
    Image: explorer.exe
    VadRoot e000012601a35e70 Vads 201 Clone 0 Private 917. Modified 2198. Locked 0.
...
```

使用して、 [ **! vad** ](-vad.md)プロセスに関連付けられている VAD ツリー リストを拡張します。 これらの Vad というラベルの付いた"EXECUTE\_WRITECOPY"コード モジュールに属しています。

```dbgcmd
kd> !vad e000012601a35e70
VAD     level      start      end    commit
...
e0000126019f9790 ( 6)      3fff0    3fff7        -1 Private      READONLY
e000012601be1080 ( 7)   37d9bd30 37d9bd3e         2 Mapped  Exe  EXECUTE_WRITECOPY  <-- these are DLLs
e000012600acd970 ( 5)   37d9bec0 37d9bece         2 Mapped  Exe  EXECUTE_WRITECOPY
e000012601a5cba0 ( 7)   37d9c910 37d9c924         2 Mapped  Exe  EXECUTE_WRITECOPY
...
```

使用して、 [ **! vad** ](-vad.md)関心のある DLL を保持するアウト ページ メモリのサイズと開始アドレスを検索するには、もう一度拡張機能。 これは、適切な DLL が検出されたことを確認します。

```dbgcmd
kd> !vad e000012601be1080 1

VAD @ e000012601be1080
  Start VPN:      37d9bd30  End VPN: 37d9bd3e  Control Area:  e00001260197b8d0
  First ProtoPte: e0000006013e00a0  Last PTE fffffffffffffffc  Commit Charge         2 (2.)
  Secured.Flink          0  Blink           0  Banked/Extend:        0
  File Offset   0
   ImageMap ViewShare EXECUTE_WRITECOPY

...
        File: \Windows\System32\ExplorerFrame.dll
```

0x37D9BD30 - ここでは、"開始 VPN"フィールドでは、開始仮想ページ番号を示します。 これは、ページ サイズを乗算することで実際のアドレスに変換する必要があります。 使用することができます、 [**でしょうか。(式の評価)** ](---evaluate-expression-.md) 0x2000 で、コンピューターの例では、Itanium ベースのページ サイズは、この値を乗算に使用するコマンドに由来します。

```dbgcmd
kd> ? 37d9bd3e*2000 
Evaluate expression: 7676040298496 = 000006fb`37a7c000
```

範囲のサイズをバイトに変換できます。

```dbgcmd
kd> ? 37d9bd3e-37d9bd30+1 <--   computes the number of pages
Evaluate expression: 15 = 00000000`0000000f
kd> ? f*2000
Evaluate expression: 122880 = 00000000`0001e000        
```

ExplorerFrame.dll がアドレス 0x000006Fb で起動するよう\`37A7C000 0x1E000 バイトが大きとします。 そのシンボルを読み込むことができます。

```dbgcmd
kd> .reload /f ExplorerFrame.dll=6fb`37a7c000,1e000
```

 

 





