---
title: Unidrv/PScript5 XPSDrv UI 動作変更
description: Unidrv/PScript5 XPSDrv UI 動作変更
ms.assetid: 7c594f40-8e75-4c8b-a60e-42f74116c75f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1395d36098f6eeab848fde8b80ff1aaf13a91b0f
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463872"
---
# <a name="unidrvpscript5-xpsdrv-ui-behavior-changes"></a>Unidrv/PScript5 XPSDrv UI 動作変更


XPSDrv モードで実行されている Unidrv/PScript5 ドライバーがドライバーの既定 UI の動作の変更に、次の主要なが作成されます。 (次の表に"PS のみ"方法動作の変更は PScript5 ドライバーに固有です。 "Unidrv のみ"の意味、動作の変更は、Unidrv ドライバーに固有です。 これらのフレーズの両方が表示されない場合、動作の変更に適用 Unidrv と PScript5 ドライバー)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>UI</th>
<th>XPSDrv 以外の動作</th>
<th>XPSDrv 動作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Orientation</p>
<p>(<strong>レイアウト</strong> タブ)</p></td>
<td><p>(PS のみ)ハード コーディングされた UI では、次の 3 つのオプションがあります。縦、横、および横置きに回転します。</p></td>
<td><p>(PS のみ)印刷の向きのハード コーディングされた UI は表示されません。</p></td>
</tr>
<tr class="even">
<td><p>コピーの数</p>
<p>(<strong>詳細</strong> タブ)</p></td>
<td><p>(Unidrv のみ)GPD ファイルに"Collate"機能がない限り、常にコピー数の UI が表示されます"<em>ConcealFromUI?。TRUE"。</p>
<p>(Unidrv のみ)EMF が有効になっている、コピー数の UI が 9999 の最大値の上限がありますにハードコーディングまたは GPD ファイルの指定したときに * MaxCopies 値。</p>
<p>(Unidrv のみ)コピーの数が GPD ファイルの上限で EMF を無効にすると、* MaxCopies 値。</p>
<p>(PS のみ)ハード コーディング 9999 を上限と、コピー数の UI が常に表示されます。</p></td>
<td><p>(Unidrv のみ)コピー数の UI は、EMF 無効になっている XPSDrv 以外の動作と同様に動作します。</p>
<p>(PS のみ)PPD ファイルで指定されている上限コピー カウントは常に表示 * MSXPSMaxCopies 値。 PPD ファイルが指定されていない場合、上限が 1 に設定 * MSXPSMaxCopies します。</p></td>
</tr>
<tr class="odd">
<td><p>部単位で印刷</p>
<p>(<strong>詳細</strong> タブ)</p></td>
<td><p>EMF が有効にすると、部単位で印刷 UI (つまりコピー数の横にあるチェック ボックス) が表示されるハードコーディングします。</p>
<p>EMF を無効にすると、丁合いが GPD または PPD ファイルとしてサポートされている機能では、"Collate"を指定して、"Collate"GPD または PPD 機能は、任意のデバイス設定の機能によって制約されない場合にのみ表示されます。</p></td>
<td><p>部単位で印刷 UI は、EMF 無効になっている XPSDrv 以外の動作と同様に動作します。</p></td>
</tr>
<tr class="even">
<td><p>色</p>
<p>(<strong>用紙/品質</strong> タブ)</p></td>
<td><p>(Unidrv のみ)GPD 返さ機能に 1 つの色のオプションがあるかどうかは、黒と白の UI の選択と色が表示されます。</p></td>
<td><p>(Unidrv のみ)黒と白の UI の選択と色が GPD 返さ機能の 1 つの色オプションの場合、および返さ機能が指定されていない場合に示すように"</em>ConcealFromUI?。TRUE"です。</p></td>
</tr>
<tr class="odd">
<td><p>ICM の方法、ICM の目的</p>
<p>(<strong>詳細</strong> タブ)</p></td>
<td><p>ICM メソッドの UI が 3 つの hard0coded オプション Unidrv: ホスト、またはドライバーによって無効にします。 この UI では、1 つ以上ハード コーディングされたドライバーのオプション PScript5 デバイスによってがあります。</p>
<p>ICM の目的の UI では、ハード コーディングされた 4 つのオプションがあります。グラフィックス、画像、実証、または一致します。</p></td>
<td><p>ハード oded ICM の方法と ICM の目的の UI は表示されません。</p></td>
</tr>
<tr class="even">
<td><p>スケーリング</p>
<p>(<strong>詳細</strong> タブ)</p></td>
<td><p>Unidrv では、スケーリングの UI は表示されません。</p>
<p>PScript5 ドライバーは、ハード コーディングされた範囲 (1% ~ 1000%) でスケーリングの UI を示しています。</p></td>
<td><p>ハード コーディングされたスケーリング UI は表示されません。 汎用 GPD または PPD スケーリング機能 (高度なツリー ビューの UI で示されています) を定義またはカスタム スケーリング UI を提供することができます。</p></td>
</tr>
<tr class="odd">
<td><p>TrueType フォント</p>
<p>(<strong>詳細</strong> タブ)</p></td>
<td><p>TrueType フォントのハード コーディングされた UI では、2 つのオプションがあります。代替デバイス フォントまたはソフト フォントとしてダウンロードします。</p></td>
<td><p>TrueType フォントのハード コーディングされた UI は表示されません。</p></td>
</tr>
<tr class="even">
<td><p>シートあたりのページ</p>
<p>(<strong>レイアウト</strong> タブ)</p></td>
<td><p>Unidrv の EMF を有効にした場合、シートあたりのページ UI はハード コーディングされた 7 つのオプションを示します。1、2、4、6、9、16、および小冊子します。</p>
<p>PScript5、UI はハード コーディングされた 7 つのオプションを示します。1、2、4、6、9、16、および小冊子します。</p></td>
<td><p>シート UI あたりハード コーディングされたページは表示されません。</p></td>
</tr>
<tr class="odd">
<td><p>その他の EMF シミュレーションの機能</p>
<p>(さまざまなタブ)</p></td>
<td><p>その他の EMF シミュレーションの機能は、次の場所に表示します。</p>
<ul>
<li>[レイアウト] タブ
<ul>
<li>Winprint ベース後処理境界線 UI チェック ボックス</li>
<li>Winprint ベース ページの順序の UI の 2 つのハードコードされたオプション:前面最背面へ移動し、前面に戻ります。</li>
</ul></li>
<li>[詳細設定] タブ。
<ul>
<li>ハードコーディングされた"詳細な印刷機能"2 つのオプション:有効または無効にします。</li>
<li>Winprint ベース後処理方向 UI を 4 つのオプション:右下後、右、下に、左、下を左下にします。</li>
<li>Winprint ベース小冊子の端の UI。</li>
</ul></li>
</ul></td>
<td><p>ハード コーディングされたまたは winprint ベース EMF シミュレーション機能はありませんが表示されます。</p></td>
</tr>
<tr class="even">
<td><p>Unidrv によってレンダリング機能</p>
<p>(さまざまなタブ)</p></td>
<td><p>(Unidrv のみ)レンダリング機能には、ハード コーディングされた 2 つの場所です。品質のマクロ UI ([用紙/品質] タブ) と ([詳細設定] タブ) のグラフィックスとテキストを印刷します。</p></td>
<td><p>(Unidrv のみ)ハード コーディングされた Unidrv レンダリング機能はありませんが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p>PScript5 によってレンダリング機能</p>
<p>(<strong>詳細</strong> タブ)</p></td>
<td><p>(PS のみ)ハード コーディングされた「PostScript オプション」は次のとおりです。PostScript 出力オプション、TrueType フォント ダウンロード オプション、PostScript 言語レベルでは、PostScript エラー ハンドラー、ミラー化された出力は、負の値の出力を送信します。</p></td>
<td><p>(PS のみ)PS レンダリングのハード コーディングされた機能はありませんが表示されます。</p></td>
</tr>
<tr class="even">
<td><p>用紙トレイ割り当てテーブル</p>
<p>(<strong>DeviceSettings</strong>  タブ)</p></td>
<td><p>用紙トレイの割り当てのテーブルは管理者用紙トレイの割り当てを選択するため常に表示されます。</p></td>
<td><p>Core Unidrv または PScript5 ドライバーは、用紙トレイ割り当てテーブルの UI は表示されません。 カスタム UI を行うことができます。</p></td>
</tr>
<tr class="odd">
<td><p>フォント代替表</p>
<p>(<strong>DeviceSettings</strong>  タブ)</p></td>
<td><p>フォント代替表は、TrueType フォントからデバイスへのフォントの置き換えを選択する管理者を有効にする常に表示されます。</p></td>
<td><p>Core Unidrv または PScript5 ドライバーは、フォント代替表 UI は表示されません。 ベンダーのプラグインでは、独自のカスタム UI を提供できます。</p></td>
</tr>
<tr class="even">
<td><p>Unidrv によってデバイスの機能</p>
<p>(<strong>DeviceSettings</strong>  タブ)</p></td>
<td><p>(Unidrv のみ)ハード コーディングされた機能には UI が含まれています</p>
<p>フォントのカートリッジまたは外部のフォント インストーラー。</p></td>
<td><p>(Unidrv のみ)Unidrv デバイスのハード コーディングされた機能はありませんが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p>PScript5 によってデバイスの機能</p>
<p>(<strong>DeviceSettings</strong>  タブ)</p></td>
<td><p>(PS のみ)ハード コーディングされた機能には、UI が含まれています。PostScript の使用可能なメモリ、出力のプロトコル前に、/後に CTRL-D を送信、灰色のテキストに変換、グレー グラフィックスに変換、ユーロ通貨記号、ジョブのタイムアウト、待機のタイムアウト、アウトラインとしてダウンロードするフォントの最小サイズおよび最大のフォント サイズをビットマップとしてダウンロードする追加します。</p></td>
<td><p>(PS のみ)PS デバイスのハード コーディングされた機能はありませんが表示されます。</p></td>
</tr>
</tbody>
</table>

 

 

 




