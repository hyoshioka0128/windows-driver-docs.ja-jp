---
title: 接続とファイル構造管理
description: 接続とファイル構造管理
ms.assetid: 3695cab3-6751-48ee-8b11-e70c2bceab29
keywords:
- データ構造の WDK ファイルシステム
- RDBSS WDK ファイルシステム、接続およびファイル構造
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、接続とファイルの構造
- 接続構造 (WDK RDBSS)
- ファイル構造の WDK RDBSS
- 構造の WDK RDBSS
- 接続情報 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05810433778c748bc5996cebfaffcff5d6f06644
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841463"
---
# <a name="connection-and-file-structure-management"></a>接続とファイル構造管理


## <span id="ddk_connection_and_file_structure_management_if"></span><span id="DDK_CONNECTION_AND_FILE_STRUCTURE_MANAGEMENT_IF"></span>


接続とファイル構造を管理するために RDBSS で使用される基本的なデータ構造は6つあります。 これらのデータ構造は、RDBSS とさまざまなネットワークミニリダイレクターによって内部的に使用されます。 これらのデータ構造には、2つのバージョンがあります。 ネットワークミニリダイレクターのバージョンには、ネットワークミニリダイレクタードライバーによって操作できるフィールドが含まれています。 これらのデータ構造のネットワークミニリダイレクターバージョンは、MRX\_ プレフィックスで始まります。 RDBSS バージョンには、RDBSS によってのみ操作できる追加フィールドが含まれています。

これらの6つの基本的なデータ構造は次のとおりです。

-   SRV\_呼び出し--サーバー呼び出しコンテキスト。 この構造は、リモートサーバーの抽象化を提供します。

-   NET\_ROOT--net root。 この構造は、共有への接続を抽象化します。

-   V\_NET\_ROOT--net ルートのビュー (仮想 netroots とも呼ばれます)。

-   FCB--ファイル制御ブロック。 この構造体は、共有上の開いているファイルを表します。

-   SRV\_開いているサーバー側のコンテキストを開きます。 この構造体は、サーバー上の開いているハンドルをカプセル化します。

-   FOBX--ファイルオブジェクト拡張子。 この構造体は、[**ファイル\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_object)構造の RDBSS 拡張です。

これらのデータ構造は、次の階層で構成されています。

```cpp
                SRV_CALL 
     FCB   <------> NET_ROOT
        SRV_OPEN  <---> V_NET_ROOT
            FOBX
                FILE_OBJECT
```

カーネルファイルシステムの呼び出しに応答して、RDBSS は、通常は FOBX 構造体を除き、前述のすべての構造を使用してネットワークミニリダイレクタードライバーを作成し、終了します。 そのため、ネットワークミニリダイレクタードライバーは通常、接続とファイル構造の管理に使用されるいくつかの RDBSS ルーチンのみを呼び出します。 これらのルーチンのほとんどは、RDBSS によって内部的に呼び出されます。

これらのすべてのデータ構造は参照カウントされます。 データ構造の参照カウントは次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">データ構造</th>
<th align="left">参照カウントの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SRV_CALL</p></td>
<td align="left"><p>SRV_CALL を指す NET_ROOT エントリの数と、いくつかの動的な値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NET_ROOT</p></td>
<td align="left"><p>NET_ROOT をポイントする FCB エントリと V_NET_ROOT エントリの数と、いくつかの動的な値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>V_NET_ROOT</p></td>
<td align="left"><p>V_NET_ROOT を指す SRV_OPEN エントリの数と、いくつかの動的な値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FCB</p></td>
<td align="left"><p>FCB を指す SRV_OPEN エントリの数と、いくつかの動的な値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SRV_OPEN</p></td>
<td align="left"><p>SRV_OPEN を指す FOBX エントリの数と、いくつかの動的な値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FOBX</p></td>
<td align="left"><p>いくつかの動的な値。</p></td>
</tr>
</tbody>
</table>

 

どちらの場合も、動的な値は、その構造体を逆参照せずに参照した呼び出し元の数を参照します。 参照カウントの静的部分は、ルーチン自体によって管理されます。 たとえば、 [**RxCreateNetRoot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatenetroot)は、関連付けられている SRV\_呼び出し構造の参照カウントをインクリメントします。

参照呼び出しと成功した参照は、参照カウントをインクリメントします。逆参照呼び出しでは、カウントをデクリメントします。 ルーチン呼び出しの作成では、構造体を割り当て、参照カウントを1に設定します。

任意のデータ構造に関連付けられている参照カウントは、少なくとも1と、それに関連付けられている次の下位レベルのデータ構造のインスタンス数を加算した値になります。 たとえば、2つの NET\_ルートが関連付けられている SRV\_呼び出しに関連付けられている参照カウントは、少なくとも3です。 RDBSS internal **NameTable**構造体と、次の下位レベルのデータ構造によって保持されている参照に加えて、追加の参照が取得されている可能性があります。

これらの制限により、次のレベルにあるすべてのデータ構造が完了するか、その参照が解放されるまで、特定のレベルのデータ構造を完了 (解放され、関連するメモリブロックが解放される) にすることはできません。 たとえば、FCB への参照が保持されている場合、その参照に関連付けられている V\_NET\_ルート、NET\_ROOT、および SRV\_呼び出し構造に安全にアクセスできます。

ネットワークミニリダイレクターと RDBSS の間のインターフェイスで使用される2つの重要な抽象化は、SRV\_呼び出しと NET\_ルート構造です。 SRV\_呼び出し構造は、接続が確立されているサーバーに関連付けられたコンテキストに対応します。また、NET\_ルート構造は、サーバー上の共有に対応します (これは、ネットワークミニリダイレクターによって要求された名前空間の一部としても表示される可能性があります)。

SRV\_呼び出しと NET\_ルート構造の作成には、通常、少なくとも1つのネットワークラウンドトリップが必要です。 非同期操作を続行するために、これらの操作は2フェーズのアクティビティとしてモデル化されています。 SRV\_呼び出しと NET\_ルート構造を作成するためにネットワークミニリダイレクターにコールダウンするたびに、ネットワークミニリダイレクターから RDBSS への呼び出しが行われ、要求の完了ステータスが通知されます。 現時点では、これらは同期です。

SRV\_呼び出し構造の作成は、RDBSS がサーバーとの接続を確立するために多数のネットワークミニリダイレクターから選択する必要があるという事実により、さらに複雑になります。 RDBSS を展開するネットワークミニリダイレクターを選択する際の柔軟性を最大限に高めるために、SRV\_呼び出し構造の作成には3番目のフェーズがあります。このフェーズでは、RDBSS がネットワークミニリダイレクターに勝者を通知します。 失われたすべてのネットワークミニリダイレクターは、関連付けられているコンテキストを破棄します。

このセクションでは、次のトピックについて説明します。

[SRV\_呼び出しの構造体](the-srv-call-structure.md)

[NET\_のルート構造](the-net-root-structure.md)

[V\_NET\_ルート構造](the-v-net-root-structure.md)

[FCB 構造体](the-fcb-structure.md)

[SRV\_オープン構造](the-srv-open-structure.md)

[FOBX 構造体](the-fobx-structure.md)

[接続とファイル構造のロック](connections-and-file-structure-locking.md)

[接続およびファイル制御ブロックの管理ルーチン](connection-and-file-control-block-management-routines.md)

 

 




