---
title: 接続とファイル構造管理
description: 接続とファイル構造管理
ms.assetid: 3695cab3-6751-48ee-8b11-e70c2bceab29
keywords:
- データ構造体の WDK ファイル システム
- RDBSS WDK ファイル システム、接続およびファイル構造
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、接続およびファイル構造
- 接続が WDK RDBSS 構造体します。
- ファイル構造 WDK RDBSS
- WDK RDBSS 構造体
- WDK RDBSS の接続情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26e1683aee9da29d2514b8c193983bdf92fa0d94
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351419"
---
# <a name="connection-and-file-structure-management"></a>接続とファイル構造管理


## <span id="ddk_connection_and_file_structure_management_if"></span><span id="DDK_CONNECTION_AND_FILE_STRUCTURE_MANAGEMENT_IF"></span>


接続およびファイル構造を管理するために RDBSS によって使用される 6 つの基本的なデータ構造があります。 これらのデータ構造は、さまざまなネットワーク ミニ-リダイレクターおよび RDBSS によって内部的に使用されます。 これらのデータ構造の 2 つのバージョンがあります。 ネットワークのミニ リダイレクター バージョンには、ネットワークのミニ リダイレクター ドライバーによって操作できるフィールドが含まれています。 これらのデータ構造のネットワークのミニ リダイレクター バージョン、MRX で始まる\_プレフィックス。 RDBSS バージョンには、のみ RDBSS によって操作できる追加のフィールドが含まれています。

これら 6 つの基本的なデータ構造は次のとおりです。

-   SRV\_呼び出し--サーバー呼び出しコンテキスト。 この構造体は、リモート サーバーの抽象化を提供します。

-   NET\_ルート - net ルート。 この構造体には、共有への接続が抽象化します。

-   V\_NET\_ルート-(仮想 netroots とも呼ばれる)、net ルートのビュー。

-   FCB--ファイル制御ブロックします。 この構造体は、共有上の開いているファイルを表します。

-   SRV\_オープン - サーバー側のコンテキストを開く。 この構造体には、サーバー上の開いているハンドルがカプセル化します。

-   FOBX--ファイル オブジェクトの拡張機能。 この構造体は RDBSS の拡張機能、 [**ファイル\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff545834)構造体。

これらのデータ構造は、次の階層に分類されます。

```cpp
                SRV_CALL 
     FCB   <------> NET_ROOT
        SRV_OPEN  <---> V_NET_ROOT
            FOBX
                FILE_OBJECT
```

ファイル システムのカーネルの呼び出しに応えて、RDBSS 通常を作成し、ネットワークのミニ リダイレクター ドライバーを終了 FOBX 構造体を除くすべての前に説明した構造体。 これで、接続およびファイル構造の管理に使用される RDBSS ルーチンのいくつかのネットワークのミニ リダイレクター ドライバーは通常呼び出し。 これらのルーチンのほとんどは RDBSS によって内部的に呼び出されます。

これらのデータ構造のすべては、カウントされた参照です。 データ構造の参照カウントは次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">データ構造体</th>
<th align="left">参照カウントの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SRV_CALL</p></td>
<td align="left"><p>SRV_CALL、およびいくつかの動的な値を指す NET_ROOT エントリの数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NET_ROOT</p></td>
<td align="left"><p>FCB のエントリと NET_ROOT、およびいくつかの動的な値を指す V_NET_ROOT エントリの数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>V_NET_ROOT</p></td>
<td align="left"><p>V_NET_ROOT、およびいくつかの動的な値を指す SRV_OPEN エントリの数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FCB</p></td>
<td align="left"><p>FCB、およびいくつかの動的な値を指す SRV_OPEN エントリの数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SRV_OPEN</p></td>
<td align="left"><p>SRV_OPEN、およびいくつかの動的な値を指す FOBX エントリの数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FOBX</p></td>
<td align="left"><p>いくつかの動的な値。</p></td>
</tr>
</tbody>
</table>

 

各ケースでは、動的な値は、それを逆参照、構造体が参照されている呼び出し元の数を示します。 参照カウントの静的な部分は、ルーチン自体によって管理されます。 たとえば、 [ **RxCreateNetRoot** ](https://msdn.microsoft.com/library/windows/hardware/ff554366) 、関連付けられている SRV の参照カウントをインクリメント\_呼び出し構造体。

参照呼び出しと成功した参照; 参照カウントをインクリメントします。カウントの呼び出しをデクリメントを逆参照します。 ルーチンの呼び出しが、構造体を割り当て、および参照カウントを 1 に設定を作成します。

すべてのデータ構造に関連付けられている参照カウントは、少なくとも 1 と、関連付けられている [次へ] の下のレベルのデータ構造体のインスタンスの数です。 たとえば、参照カウントに関連付けられている、SRV\_呼び出すには、NET の 2 つ持つ\_それに関連付けられているルートは少なくとも 3。 内部の RDBSS によって保持されている参照に加えて**NameTable**構造と、次のデータ構造をレベル削減が取得されているその他の参照があります。

これらの制限によって、任意の特定のレベルでのデータ構造を確定できません (リリースおよび関連するメモリ ブロックが解放される) までファイナライズされているすべての下のレベルでデータ構造、またはの参照を解放します。 たとえば、FCB への参照が保持されている場合も安全です、V へのアクセスに\_NET\_ルート、NET\_ルートであり、SRV\_呼び出し構造が関連付けられています。

ネットワークのミニ リダイレクターと RDBSS 間のインターフェイスで使用される 2 つの重要な抽象化は SRV\_呼び出しと NET\_ルート構造体。 SRV\_呼び出し構造体に対応する、接続が確立されている、サーバーに関連付けられたコンテキストと、NET\_ルート構造体に対応する (これが見ることも、名前空間の一部としてサーバー上の共有これがによって要求されてネットワーク ミニリダイレクター)。

SRV の作成\_呼び出しと NET\_ルート構造体通常では、少なくとも 1 つのネットワーク ラウンド トリップします。 非同期操作を続行できるを提供するには、これらの操作は、2 フェーズのアクティビティとしてモデル化されます。 各呼び出しのリスト、SRV を作成するため、ネットワーク ミニ リダイレクター\_呼び出しと、NET\_ルート構造体が付属して、call-up ミニリダイレクター ネットワークからの要求の完了ステータスを通知する RDBSS にします。 現在これらは同期です。

作成、SRV\_呼び出し構造が、RDBSS は、サーバーとの接続を確立するためにさまざまなネットワークのミニ リダイレクターから選択する必要があるという事実によってさらに複雑です。 最大限の柔軟性、SRV の作成を展開する必要があるネットワーク ミニ-リダイレクターを選択すると、RDBSS を提供する\_呼び出し構造体には、RDBSS が優勝者のネットワークのミニ リダイレクターに通知する 3 番目のフェーズが含まれます。 すべての優先ネットワーク ミニ-リダイレクターは、関連付けられたコンテキストを破棄します。

このセクションでは、次のトピックについて説明します。

[SRV\_呼び出し構造](the-srv-call-structure.md)

[NET\_ルート構造体](the-net-root-structure.md)

[V\_NET\_ルート構造体](the-v-net-root-structure.md)

[FCB 構造体](the-fcb-structure.md)

[SRV\_オープン構造体](the-srv-open-structure.md)

[FOBX 構造体](the-fobx-structure.md)

[接続およびファイルのロック構造体。](connections-and-file-structure-locking.md)

[接続し、ファイル制御ブロック管理ルーチン](connection-and-file-control-block-management-routines.md)

 

 




