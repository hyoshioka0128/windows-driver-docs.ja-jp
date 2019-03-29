---
title: ファイル システム フィルター ドライバー用のロード順序グループ
description: ファイル システム フィルター ドライバー用のロード順序グループ
ms.assetid: 57c9e4c6-186c-464f-ac83-c0669d46b189
keywords:
- フィルター ドライバー WDK ファイル システム、ドライバーの読み込み
- ファイル システム フィルター ドライバー WDK、ドライバーの読み込み
- ドライバー WDK ファイル システムの読み込み
- ドライバー WDK ファイル システムの読み込み
- 注文グループ WDK ファイル システムを読み込む
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4ff7a0852955c73cb1df4018a744f853b7fa700
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464264"
---
# <a name="load-order-groups-for-file-system-filter-drivers"></a>ファイル システム フィルター ドライバー用のロード順序グループ


## <span id="ddk_file_system_filter_driver_load_order_groups_if"></span><span id="DDK_FILE_SYSTEM_FILTER_DRIVER_LOAD_ORDER_GROUPS_IF"></span>


Microsoft Windows XP およびそれ以降のオペレーティング システム専用のセットを提供ロード順序グループのシステムの起動時に読み込まれているファイル システム フィルター ドライバー。 Windows XP より前に、のオペレーティング システムでフィルター ドライバーは、「フィルター」のみを使用でき、"file system"の読み込み順序グループ。

フィルターは、既存のファイル システム ドライバー スタックの先頭にのみアタッチでき、スタックの途中でアタッチできません。 その結果、ロード順序グループはファイル システム フィルター ドライバー、重要な前フィルター ドライバーが読み込まれるため、小さいにアタッチできますファイル システム ドライバー スタック上。

ロード順序グループの詳細については、次の規則は、ファイル システム フィルター ドライバーが読み込まれるときに決定します。

-   特定のロード順序グループを指定するファイル システム フィルター ドライバーは、そのグループ内の他のフィルター ドライバーと同時に読み込まれます。

-   各ロード順序グループ内では、フィルター ドライバーはランダムな順序で読み込まれます。

-   ファイル システム フィルター ドライバーがロード順序グループを指定しない場合は、ロード順序グループを指定して型をすべて同じの他のドライバーの開始後に読み込まれます。

次の表は、ファイル システム フィルター ドライバーのシステム定義のロード順序グループを一覧表示します。 ロード順序グループごとに、ロード順序グループ列には、そのグループを指定する値が含まれています、 **LoadOrderGroup**内のエントリ、 [**バージョン セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547502)フィルターの INF ファイルです。

読み込まれた順の逆であると、スタックに表示されると、ロード順序グループが表示されることに注意してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ロード順序グループ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>フィルター</p></td>
<td align="left"><p>このグループでは、Windows 2000 で使用可能な以前 [フィルター] のロード順序グループと同じです。 このグループは、最後に読み込まされ、したがって、ファイル システム遠いアタッチします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 上部</p></td>
<td align="left"><p>このグループは、何より FSFilter 他の種類をアタッチする必要がありますフィルター ドライバーに対して提供されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 利用状況モニター</p></td>
<td align="left"><p>このグループには、フィルター ドライバー確認し、ファイル I/O レポートにはが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 削除の取り消し</p></td>
<td align="left"><p>このグループには、削除されたファイルを回復するフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter ウイルス対策</p></td>
<td align="left"><p>このグループには、検出して、ファイル I/O 中にウイルスを駆除するフィルターが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter レプリケーション</p></td>
<td align="left"><p>このグループには、リモート サーバーにファイル データをレプリケートするフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 継続的なバックアップ</p></td>
<td align="left"><p>このグループには、バックアップ メディアにファイル データをレプリケートするフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter コンテンツこだわりの検索</p></td>
<td align="left"><p>このグループには、特定のファイルまたはファイルの内容の作成を禁止するフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter クォータの管理</p></td>
<td align="left"><p>このグループには、拡張ファイル システムのクォータを提供するフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter システムの回復</p></td>
<td align="left"><p>このグループには、システムの復元 (SR) フィルターなどのオペレーティング システムの整合性を維持するために操作を実行するフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter クラスター ファイル システム</p></td>
<td align="left"><p>このグループには、ネットワーク経由でファイル サーバーのメタデータを提供する製品で使用されるフィルター ドライバーが含まれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter HSM</p></td>
<td align="left"><p>このグループには、階層型記憶域の管理を実行するフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter イメージング</p></td>
<td align="left"><p>このグループには、仮想名前空間を提供する ZIP に似たフィルター ドライバーが含まれています。</p>
<p>このグループの読み込みは、Windows Vista およびそれ以降のバージョンのオペレーティング システムで利用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 圧縮</p></td>
<td align="left"><p>このグループには、ファイルのデータ圧縮を実行するフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 暗号化</p></td>
<td align="left"><p>このグループには、暗号化、およびファイル I/O 中にデータを復号化するフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 仮想化</p></td>
<td align="left"><p>このグループには、Windows Vista で追加された、少なくとも承認されたユーザー (LUA) フィルター ドライバーなどのファイルのパスを仮想化フィルター ドライバーが含まれています。</p>
<p>このグループの読み込みは、Windows Vista およびそれ以降のバージョンのオペレーティング システムで利用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 物理クォータの管理</p></td>
<td align="left"><p>このグループには、物理ブロックの数を使用してクォータを管理するフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>開いている FSFilter ファイル</p></td>
<td align="left"><p>このグループには、既に開いているファイルのスナップショットを提供するフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter セキュリティ強化</p></td>
<td align="left"><p>このグループには、ロックダウンを適用するフィルター ドライバーが含まれていて、強化されたアクセス制御リスト (Acl)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter コピー防止</p></td>
<td align="left"><p>このグループには、メディア上の帯域外のデータをチェックするフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 下部</p></td>
<td align="left"><p>このグループは、他のすべての FSFilter 型の下にアタッチする必要がありますフィルター ドライバーに対して提供されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter システム</p></td>
<td align="left"><p>内部使用のために予約済みです。 このグループには、HSM と SIS フィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter インフラストラクチャ</p></td>
<td align="left"><p>内部使用のために予約済みです。 このグループは、ファイル システムに最も近い接続および最初を読み込みます。</p></td>
</tr>
</tbody>
</table>

 

 

 




