---
title: ミニフィルター ドライバー用のロード順序グループと高度
description: ミニフィルター ドライバー用のロード順序グループと高度
ms.assetid: be8f18fe-c80b-44a3-b0c3-f2f630142180
keywords:
- 高度 WDK ファイルシステムミニフィルター
- 読み込み順序グループ WDK ファイルシステム
- WDK ファイルシステムの種類の開始
- ドライバーの開始の種類 WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a511a319fbbbc5c24379c210d6741b6e258c5a3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841141"
---
# <a name="load-order-groups-and-altitudes-for-minifilter-drivers"></a>ミニフィルター ドライバー用のロード順序グループと高度


Windows では、システムの起動時に読み込まれるファイルシステムフィルタードライバーとミニフィルタードライバーに対して、一連の専用の読み込み順序グループを使用します。

レガシファイルシステムフィルタードライバーは、既存のファイルシステムドライバースタックの一番上にのみアタッチでき、スタックの途中でアタッチすることはできません。 このため、従来のファイルシステムフィルタードライバーでは、ドライバーおよび読み込み順序グループの開始の種類が重要です。以前のフィルタードライバーが読み込まれるため、ファイルシステムのドライバースタックに接続することができます。

ドライバーは、ドライバーの開始の種類に基づいて最初に読み込まれます。これは、システムの起動フェーズを表します。 開始の種類の詳細については、「ドライバーの起動の種類」を[参照してください。](what-determines-when-a-driver-is-loaded.md) スタートアップの種類のサービス\_起動\_を指定するすべてのファイルシステムフィルタードライバーとミニフィルタードライバーは、スタートアップの種類がサービス\_システム\_開始またはサービス\_自動\_開始するドライバーの前に読み込まれます。 スタートアップの種類は、ミニフィルタードライバーをインストールするために使用される INF ファイルの ServiceInstall セクションの**starttype**エントリによって指定されます。 [開始の種類] カテゴリごとに、[読み込み順序] グループによって、ファイルシステムフィルタードライバーとミニフィルタードライバーがいつ読み込まれるかが決定されます。

ミニフィルタードライバーは、いつでも読み込むことができます。 従来のファイルシステムフィルタードライバーとの相互運用性を実現するために、ミニフィルタードライバーでは、負荷順序グループの概念が必要です。 すべてのミニフィルタードライバーには、*高度*と呼ばれる一意の識別子が必要です。 ミニフィルタードライバーの高度は、ミニフィルタードライバーが読み込まれるときに、i/o スタック内の他のミニフィルタードライバーとの相対的な位置を定義します。 高度は、10進数として解釈される無限精度の文字列です。 数値の高度が低いミニフィルタードライバーは、数値が大きいミニフィルタードライバーの下に i/o スタックに読み込まれます。

各読み込み順序グループには、高度な範囲が定義されています。 ミニフィルタードライバーへの高度な割り当ては、Microsoft によって管理されます。 ミニフィルタードライバーの高度を要求するには、に電子メールメッセージを送信して、割り当てられているかどうかを確認 <fsfcomm@microsoft.com> ます。

ミニフィルタードライバーでは、読み込み順序グループを表す高度な範囲の高度な値を指定する必要があります。 ミニフィルタードライバーの高度値は、ミニフィルタードライバーのインストールに使用される INF ファイルの文字列セクションのインスタンス定義で指定されます。 インスタンス定義は、 [**FLT\_REGISTRATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)構造体の[**instancesetupcallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_setup_callback)ルーチンの呼び出しで指定することもできます。 ミニフィルタードライバーには、複数のインスタンスと高度を定義できます。 これらのインスタンス定義は、すべてのボリュームに適用されます。

次のルールでは、開始の種類と読み込み順序のグループについて、ミニフィルタードライバーがいつ読み込まれるかを決定します。

-   特定の開始の種類と負荷の順序のグループを指定するミニフィルタードライバーは、その開始の種類と負荷の順序グループの他のファイルシステムフィルタードライバーおよびミニフィルタードライバーと同時に読み込まれます。

-   各読み込み順序グループ内で、ファイルシステムフィルタードライバーとミニフィルタードライバーは、通常、ランダムな順序で読み込まれます。 これにより、ドライバーがインストールされた順序に基づいてドライバーが読み込まれます。

-   ファイルシステムフィルタードライバーまたはミニフィルタードライバーによって、読み込み順序グループが指定されていない場合は、同じスタートアップの種類の他のすべてのドライバーが読み込み順序グループを指定した後に読み込まれます。

次の表に、システム定義の読み込み順序グループとミニフィルタードライバーの高度な範囲を示します。 各読み込み順序グループについて、[読み込み順序グループ] 列には、ミニフィルターの INF ファイルの ServiceInstall セクションの**Loadordergroup**エントリでそのグループに指定する値が含まれています。 [高度範囲] 列には、特定の負荷順序グループの高度な範囲が含まれます。 ミニフィルタードライバーでは、適切な負荷順序のグループまたはグループ内の Microsoft からの高度な割り当てを要求する必要があります。

読み込み順序グループと高度な範囲は、スタックに表示されているとおりに一覧表示されます。これは、読み込まれた順序の逆です。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">読み込み順序グループ</th>
<th align="left">高度範囲</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>フィルター</p></td>
<td align="left"><p>420000-429999</p></td>
<td align="left"><p>このグループは、Windows 2000 以前で使用できたフィルター読み込み順序グループと同じです。 このグループは最後に読み込まれるため、ファイルシステムから最も遠いものがアタッチされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>上にある FSFilter</p></td>
<td align="left"><p>400000-409999</p></td>
<td align="left"><p>このグループは、他のすべての FSFilter の種類の上にアタッチする必要があるフィルタードライバー用に用意されています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 利用状況モニター</p></td>
<td align="left"><p>360000-389999</p></td>
<td align="left"><p>このグループには、ファイル i/o を監視および報告するフィルタードライバーが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter の削除の取り消し</p></td>
<td align="left"><p>340000-349999</p></td>
<td align="left"><p>このグループには、削除されたファイルを回復するフィルターが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter ウイルス対策</p></td>
<td align="left"><p>320000-329999</p></td>
<td align="left"><p>このグループには、ファイル i/o 中にウイルスを検出して駆除するフィルタードライバーが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter レプリケーション</p></td>
<td align="left"><p>300000-309999</p></td>
<td align="left"><p>このグループには、ファイルデータをリモートサーバーにレプリケートするフィルタードライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 連続バックアップ</p></td>
<td align="left"><p>280000-289999</p></td>
<td align="left"><p>このグループには、ファイルデータをバックアップメディアにレプリケートするフィルタードライバーが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter コンテンツスクリーナー</p></td>
<td align="left"><p>260000-269999</p></td>
<td align="left"><p>このグループには、特定のファイルまたはファイルコンテンツを作成できないようにするフィルタードライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter クォータの管理</p></td>
<td align="left"><p>240000-249999</p></td>
<td align="left"><p>このグループには、拡張ファイルシステムのクォータを提供するフィルタードライバーが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter システムの回復</p></td>
<td align="left"><p>220000-229999</p></td>
<td align="left"><p>このグループには、システムの復元 (SR) フィルターなど、オペレーティングシステムの整合性を維持する操作を実行するフィルタードライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter クラスターファイルシステム</p></td>
<td align="left"><p>200000-209999</p></td>
<td align="left"><p>このグループには、ネットワーク経由でファイルサーバーのメタデータを提供する製品で使用されるフィルタードライバーが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter HSM</p></td>
<td align="left"><p>180000-189999</p></td>
<td align="left"><p>このグループには、階層型記憶域の管理を実行するフィルタードライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter イメージング</p></td>
<td align="left"><p>170000-175000</p></td>
<td align="left"><p>このグループには、仮想名前空間を提供する ZIP 形式のフィルタードライバーが含まれています。</p>
<p>この読み込みグループは、Windows Vista 以降のバージョンのオペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter の圧縮</p></td>
<td align="left"><p>160000-169999</p></td>
<td align="left"><p>このグループには、ファイルデータの圧縮を実行するフィルタードライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter の暗号化</p></td>
<td align="left"><p>140000-149999</p></td>
<td align="left"><p>このグループには、ファイル i/o 中にデータを暗号化および暗号化解除するフィルタードライバーが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter の仮想化</p></td>
<td align="left"><p>13万 ~ 139999</p></td>
<td align="left"><p>このグループには、Windows Vista で追加された承認されていないユーザー (LUA) フィルタードライバーなど、ファイルパスを仮想化するフィルタードライバーが含まれています。</p>
<p>この読み込みグループは、Windows Vista 以降のバージョンのオペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter の物理クォータ管理</p></td>
<td align="left"><p>120000-129999</p></td>
<td align="left"><p>このグループには、物理ブロック数を使用してクォータを管理するフィルタードライバーが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 開いているファイル</p></td>
<td align="left"><p>100000-109999</p></td>
<td align="left"><p>このグループには、既に開いているファイルのスナップショットを提供するフィルタードライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter セキュリティ言え</p></td>
<td align="left"><p>80000-89999</p></td>
<td align="left"><p>このグループには、ロックダウンおよび拡張アクセス制御リスト (Acl) を適用するフィルタードライバーが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter のコピー保護</p></td>
<td align="left"><p>60000-69999</p></td>
<td align="left"><p>このグループには、メディア上の帯域外データをチェックするフィルタードライバーが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>下位の FSFilter</p></td>
<td align="left"><p>40000-49999</p></td>
<td align="left"><p>このグループは、他のすべての FSFilter の種類の下に接続する必要があるフィルタードライバー用に用意されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter システム</p></td>
<td align="left"><p>20000-29999</p></td>
<td align="left"><p>内部使用のために予約済みです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter インフラストラクチャ</p></td>
<td align="left"></td>
<td align="left"><p>内部使用のために予約済みです。 このグループは最初に読み込まれるため、ファイルシステムに最も近い場所にアタッチされます。</p></td>
</tr>
</tbody>
</table>

 

 

 




