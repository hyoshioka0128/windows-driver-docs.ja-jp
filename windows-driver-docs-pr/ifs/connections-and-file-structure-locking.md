---
title: 接続とファイル構造のロック
description: 接続とファイル構造のロック
ms.assetid: 7286a34f-db8f-4b0a-ab7f-674b9dc641a8
keywords:
- ロックの WDK RDBSS
- デバイスごとのオブジェクト テーブル WDK RDBSS
- WDK RDBSS の排他ロック
- 参照カウントの WDK RDBSS
- テーブル-NET_ROOT あたり構造 WDK RDBSS
- データ構造体の WDK ファイル システム
- RDBSS WDK ファイル システム、接続およびファイル構造
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、接続およびファイル構造
- 接続が WDK RDBSS 構造体します。
- ファイル構造 WDK RDBSS
- WDK RDBSS 構造体
- WDK RDBSS の接続情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49485a815419be3905117e7bcc990bbb5e673902
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391114"
---
# <a name="connections-and-file-structure-locking"></a>接続とファイル構造のロック


## <span id="ddk_connections_and_file_structure_locking_if"></span><span id="DDK_CONNECTIONS_AND_FILE_STRUCTURE_LOCKING_IF"></span>


ロックのためでは、使用される参照テーブルの 2 つのレベルです。

-   SRV のデバイスごとのオブジェクト テーブル\_呼び出しと NET\_ルート構造体 (プレフィックス テーブル)

-   NET ごとのテーブル\_FCB 構造 (FCB テーブル) のルート構造体

これらの個別のテーブルが別のネットワーク上のディレクトリ操作を許可する\_をほぼ完全に非-妨げられること、接続が確立されると、ルート構造体。 同じネットワーク上のディレクトリ操作\_ルート構造体がただし干渉、少しの操作を行います。 次の表では、特定の操作に必要なロックについて説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">操作</th>
<th align="left">データ型</th>
<th align="left">必要なロック</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>作成または最終処理</p></td>
<td align="left"><p></p>
SRV_CALL NET_ROOT V_NET_ROOT</td>
<td align="left"><p>NetName テーブルに対する排他ロック (RxContext - の TableLock フィールド&gt;RxDeviceObject-&gt;pRxNetNameTable)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>参照を逆参照、または参照</p></td>
<td align="left"><p></p>
SRV_CALL NET_ROOT V_NET_ROOT</td>
<td align="left"><p>NetName テーブルを共有または排他ロック (RxContext - の TableLock フィールド&gt;RxDeviceObject-&gt;pRxNetNameTable)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>作成または最終処理</p></td>
<td align="left"><p></p>
FCB SRV_OPEN FOBX</td>
<td align="left"><p>FCB テーブルに対する排他ロック (NET_ROOT - の TableLock フィールド&gt;FcbTable)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>参照を逆参照、または参照</p></td>
<td align="left"><p></p>
FCB SRV_OPEN FOBX</td>
<td align="left"><p>FCB テーブルを共有または排他ロック (NET_ROOT - の TableLock フィールド&gt;FcbTable)。</p></td>
</tr>
</tbody>
</table>

 

注その操作の SRV\_現在、オープンと FOBX データ構造体には FCB データ構造の操作に必要な同じロックが必要です。 これは、アイデアを保存するメモリだけです。 Windows の将来のバージョンは、この制限を削除して、一連の共有リソースは比較的安価なレベルの衝突の可能性を減らすにされる可能性があります FCB レベルで別のリソースを追加することがあります。

行う必要があります、ロック NetName テーブルの最初のロック (FinalizeNetFcb、たとえば)、両方 FCB テーブルをロックしが必要な場合。 逆の順序でロックを解除する必要があります。

SRV\_呼び出し、NET\_ルート、および V\_NET\_ルートの作成と終了のプロセスは、取得と RDBSS NetName テーブル ロックの解放によって管理されます。

FCB の作成と終了のプロセスは、取得と NET に関連付けられている NetName テーブルのロックの解放によって管理されます\_ルート構造体。

FOBX SRVOPEN の作成とファイナライズ プロセスは、取得と FCB テーブルのロックの解放によって制御されます。

次の表は、ロックとロックの作成と、さまざまなデータ構造の最終処理を取得する必要がモードをまとめたものです。

<table>
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">操作の種類</th>
<th align="left">SRV_CALL</th>
<th align="left">NET_ROOT</th>
<th align="left">FCB</th>
<th align="left">SRV_OPEN</th>
<th align="left">FOBX</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>作成</p></td>
<td align="left"><p>NetName テーブルに排他ロック</p></td>
<td align="left"><p>NetName テーブルに排他ロック</p></td>
<td align="left"><p>FCB のテーブルに排他ロック</p></td>
<td align="left"><p>FCB のテーブルに排他ロック</p></td>
<td align="left"><p>FCB のテーブルに排他ロック</p></td>
</tr>
<tr class="even">
<td align="left"><p>最終処理します。</p></td>
<td align="left"><p>NetName テーブルに排他ロック</p></td>
<td align="left"><p>NetName テーブルに排他ロック</p></td>
<td align="left"><p>FCB のテーブルに排他ロック</p></td>
<td align="left"><p>FCB のテーブルに排他ロック</p></td>
<td align="left"><p>FCB のテーブルに排他ロック</p></td>
</tr>
</tbody>
</table>

 

参照して、これらのデータ構造体を逆参照も特定の規則に従う必要があります。

参照カウントに関連付けられているデータ構造体のいずれか 1 (ほとんどの場合、名前のテーブルによって保持されている唯一のリファレンス) を削除、ときに、データ構造体、終了処理の潜在的な候補です。 データ構造体かを確定できます直ちにまたは清掃を指定できます。 これら両方のメソッドは、RDBSS で実装されます。 逆参照時にロックの要件が満たされると、データ構造がすぐに完了しました。 1 つの例外は、遅延と (たとえば FCB 構造体の逆参照) 操作の最適化を実装します。 それ以外の場合、データ構造は、清掃マークされます。

ネットワークのミニ リダイレクターは、終了処理ルーチンを呼び出すために NetName テーブルに排他ロックが必要です。

をこれらのデータ構造のいずれかで、作成を実行するには、ネットワーク ミニ リダイレクター ドライバーは、次のようなものを実行する必要があります。

```cpp
    getshared();lookup();
    if (failed) {
        release(); getexclusive(); lookup();
            if ((failed) { create(); }
        }
    deref();
    release();
```

ロックが正常に取得されるとは、テーブルに、ノードを挿入し、ロックを解放し、サーバーが使用可能なかどうかを参照してください。 他の情報を設定し、ブロックを解除するが、同じサーバー上で待機しているすべてのユーザー、サーバーが使用可能な場合は、(、SRV\_呼び出しまたは NET\_ルート構造体)。

 

 




