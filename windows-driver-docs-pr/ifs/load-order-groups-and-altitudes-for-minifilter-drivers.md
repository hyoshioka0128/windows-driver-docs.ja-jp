---
title: ミニフィルター ドライバー用のロード順序グループと高度
description: ミニフィルター ドライバー用のロード順序グループと高度
ms.assetid: be8f18fe-c80b-44a3-b0c3-f2f630142180
keywords:
- ファイル システム ミニフィルターの高度 WDK
- 注文グループ WDK ファイル システムを読み込む
- 型の WDK ファイル システムを起動します。
- ドライバー開始の種類の WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b7f7f1a9481db9bb0281ea0679dcbe85b0926f3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376007"
---
# <a name="load-order-groups-and-altitudes-for-minifilter-drivers"></a>ミニフィルター ドライバー用のロード順序グループと高度


Windows では、ファイル システム フィルター ドライバーとシステムの起動時に読み込まれるミニフィルター ドライバーの読み込み順序グループの専用のセットを使用します。

従来のファイル システム フィルター ドライバーは、既存のファイル システム ドライバー スタックの一番上にのみアタッチでき、スタックの途中でアタッチできません。 結果として、開始ドライバーとロード順序グループの種類は従来のファイル システム フィルター ドライバー、重要な以前フィルター ドライバーが読み込まれるため、小さいにアタッチできますファイル システム ドライバー スタック上。

ドライバーでは、システムのブートのフェーズを表すと、ドライバーのスタートアップの種類に基づいて、最初に読み込まれます。 スタートアップの種類に関する詳細については、「ドライバーを開始型」を参照してください[何を決定しますと、ドライバーが読み込まれる](what-determines-when-a-driver-is-loaded.md)します。 すべてのファイル システム フィルター ドライバーとサービスの開始の種類を示すミニフィルター ドライバー\_ブート\_開始ドライバー サービスの開始の種類とする前に読み込まれる\_システム\_開始またはサービス\_自動\_を開始します。 開始の種類がで指定された、 **StartType**ミニフィルター ドライバーをインストールするために使用される INF ファイルの ServiceInstall セクション内のエントリ。 各開始の種類のカテゴリ内では、ロード順序グループは、ファイル システム フィルター ドライバーとミニフィルター ドライバーが読み込まれるときに決定します。

ミニフィルター ドライバーは、いつでも読み込むことができます。 ロード順序グループの概念が、従来のファイル システム フィルター ドライバーとの相互運用性ミニフィルター ドライバーによってまだ必要です。 ミニフィルター ドライバーと呼ばれる一意の識別子をいる必要があります*高度*します。 ミニフィルター ドライバーの高度は、ミニフィルター ドライバーが読み込まれるときに、I/O スタック内の他のミニフィルター ドライバー相対位置を定義します。 高度は、10 進数として解釈無限の有効桁数の文字列です。 高度が低い数値を含むミニフィルター ドライバーは、高い数値の値を持つミニフィルター ドライバーの下に、I/O スタックに読み込まれます。

各ロード順序グループでは、高度の定義された範囲を持ちます。 ミニフィルター ドライバーに高度の割り当ては、Microsoft によって管理されます。 ミニフィルター ドライバーの高度を要求する電子メール メッセージを送信<fsfcomm@microsoft.com>割り当てられる 1 つを要求します。

ミニフィルター ドライバーには、ロード順序グループを表す高度の範囲から高度値を指定する必要があります。 ミニフィルター ドライバーの高度の値は、ミニフィルター ドライバーのインストールに使用される INF ファイルの文字列のセクションのインスタンスの定義で指定されます。 呼び出しでインスタンスの定義を指定することも、 [ **InstanceSetupCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_instance_setup_callback)で日常的な[ **FLT\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_registration)構造体。 ミニフィルター ドライバーに対しては、複数のインスタンスと高度を定義できます。 これらのインスタンスの定義は、すべてのボリュームに適用されます。

詳細については、次の規則が型を起動し、ミニフィルター ドライバーが読み込まれるときにロード順序グループが決定します。

-   特定の開始の種類、ロード順序グループが他のファイル システム フィルター ドライバーと同時に読み込まれるとミニフィルター ドライバーには、開始の種類と、ロード順序グループを指定するミニフィルター ドライバー。

-   各ロード順序グループ内でランダムな順序でファイル システム フィルター ドライバーとミニフィルター ドライバーは一般にロードします。 通常、この結果、ドライバー、ドライバーがインストールされている順序に基づいて読み込まれています。

-   ファイル システム フィルター ドライバーまたはミニフィルター ドライバーがロード順序グループを指定していない場合は、読み込まれることすべてロード順序グループを指定して、同じ開始の種類の他のドライバー。

次の表は、システム定義の読み込み順序グループとミニフィルター ドライバー用の高度の範囲を示します。 ロード順序グループごとに、ロード順序グループ 列には、そのグループを指定する値が含まれています、 **LoadOrderGroup**ミニフィルターの INF ファイルの ServiceInstall セクションのエントリ。 高度の範囲の列には、特定のロード順序グループの高度の範囲が含まれています。 ミニフィルター ドライバーは、適切なロード順序グループまたはグループに Microsoft から高度割り当てを要求する必要があります。

読み込まれた順の逆であると、スタックに表示されると、ロード順序グループと高度の範囲が一覧表示することに注意してください。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ロード順序グループ</th>
<th align="left">高度の範囲</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>フィルター</p></td>
<td align="left"><p>420000-429999</p></td>
<td align="left"><p>このグループは、Windows 2000 で使用可能な以前の注文のグループを読み込み、フィルターと同じです。 このグループは、最後に読み込まされ、したがって、ファイル システム遠いアタッチします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 上部</p></td>
<td align="left"><p>400000-409999</p></td>
<td align="left"><p>このグループは、何より FSFilter 他の種類をアタッチする必要がありますフィルター ドライバーに対して提供されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 利用状況モニター</p></td>
<td align="left"><p>360000-389999</p></td>
<td align="left"><p>このグループには、フィルター ドライバー確認し、ファイル I/O レポートにはが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 削除の取り消し</p></td>
<td align="left"><p>340000-349999</p></td>
<td align="left"><p>このグループには、削除されたファイルを回復するフィルターが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter ウイルス対策</p></td>
<td align="left"><p>320000-329999</p></td>
<td align="left"><p>このグループには、検出して、ファイル I/O 中にウイルスを駆除するフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter レプリケーション</p></td>
<td align="left"><p>300000-309999</p></td>
<td align="left"><p>このグループには、リモート サーバーにファイル データをレプリケートするフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 継続的なバックアップ</p></td>
<td align="left"><p>280000-289999</p></td>
<td align="left"><p>このグループには、バックアップ メディアにファイル データをレプリケートするフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter コンテンツこだわりの検索</p></td>
<td align="left"><p>260000-269999</p></td>
<td align="left"><p>このグループには、特定のファイルまたはファイルの内容の作成を禁止するフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter クォータの管理</p></td>
<td align="left"><p>240000-249999</p></td>
<td align="left"><p>このグループには、拡張ファイル システムのクォータを提供するフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter システムの回復</p></td>
<td align="left"><p>220000-229999</p></td>
<td align="left"><p>このグループには、システムの復元 (SR) フィルターなどのオペレーティング システムの整合性を維持するために操作を実行するフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter クラスター ファイル システム</p></td>
<td align="left"><p>200000-209999</p></td>
<td align="left"><p>このグループには、ネットワーク経由でファイル サーバーのメタデータを提供する製品で使用されるフィルター ドライバーが含まれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter HSM</p></td>
<td align="left"><p>180000-189999</p></td>
<td align="left"><p>このグループには、階層型記憶域の管理を実行するフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter イメージング</p></td>
<td align="left"><p>170000-175000</p></td>
<td align="left"><p>このグループには、仮想名前空間を提供する ZIP に似たフィルター ドライバーが含まれています。</p>
<p>このグループの読み込みは、Windows Vista およびそれ以降のバージョンのオペレーティング システムで利用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 圧縮</p></td>
<td align="left"><p>160000-169999</p></td>
<td align="left"><p>このグループには、ファイルのデータ圧縮を実行するフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 暗号化</p></td>
<td align="left"><p>140000-149999</p></td>
<td align="left"><p>このグループには、暗号化、およびファイル I/O 中にデータを復号化するフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 仮想化</p></td>
<td align="left"><p>130000- 139999</p></td>
<td align="left"><p>このグループには、Windows Vista で追加された、少なくとも承認されたユーザー (LUA) フィルター ドライバーなどのファイルのパスを仮想化フィルター ドライバーが含まれています。</p>
<p>このグループの読み込みは、Windows Vista およびそれ以降のバージョンのオペレーティング システムで利用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 物理クォータの管理</p></td>
<td align="left"><p>120000-129999</p></td>
<td align="left"><p>このグループには、物理ブロックの数を使用してクォータを管理するフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>開いている FSFilter ファイル</p></td>
<td align="left"><p>100000-109999</p></td>
<td align="left"><p>このグループには、既に開いているファイルのスナップショットを提供するフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter セキュリティ強化</p></td>
<td align="left"><p>80000-89999</p></td>
<td align="left"><p>このグループには、ロックダウンを適用するフィルター ドライバーが含まれていて、強化されたアクセス制御リスト (Acl)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter コピー防止</p></td>
<td align="left"><p>60000-69999</p></td>
<td align="left"><p>このグループには、メディア上の帯域外のデータをチェックするフィルター ドライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 下部</p></td>
<td align="left"><p>40000-49999</p></td>
<td align="left"><p>このグループは、他のすべての FSFilter 型の下にアタッチする必要がありますフィルター ドライバーに対して提供されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter システム</p></td>
<td align="left"><p>20000-29999</p></td>
<td align="left"><p>内部使用のために予約済みです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter インフラストラクチャ</p></td>
<td align="left"></td>
<td align="left"><p>内部使用のために予約済みです。 このグループは、ファイル システムに最も近い接続および最初を読み込みます。</p></td>
</tr>
</tbody>
</table>

 

 

 




