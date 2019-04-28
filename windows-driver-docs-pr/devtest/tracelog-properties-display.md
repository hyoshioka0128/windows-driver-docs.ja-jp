---
title: Tracelog のプロパティの表示
description: Tracelog のプロパティの表示
ms.assetid: 9adfb4d5-5a0b-4e79-9aa8-ae81e2e1df3e
keywords:
- Tracelog WDK、プロパティ
- WDK、プロパティのトレース
- WDK トレースのプロパティ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de983da6a83b9c80fd4da513ca9b05af06d344d2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369718"
---
# <a name="tracelog-properties-display"></a>Tracelog のプロパティの表示

## <span id="ddk_tracelog_display_tools"></span><span id="DDK_TRACELOG_DISPLAY_TOOLS"></span>

トレース ログには、開始、停止、更新、またはクエリ、セッションのトレース セッションのプロパティが表示されます。

データの取得元イベント\_トレース\_ログ セッションのプロパティの構造体。 次の表では、表示されるフィールドについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>操作の状態</strong></p></td>
<td align="left"><p>システムによって返される状態。 ステータス メッセージとシステム エラー コードの一覧は、Microsoft Windows SDK のドキュメントを参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ロガー名</strong></p></td>
<td align="left"><p>トレース セッションの名前。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ロガー ID</strong></p></td>
<td align="left"><p>トレース セッションを識別します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ロガー スレッド ID</strong></p></td>
<td align="left"><p>トレース セッションを実行しているスレッドを識別します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>バッファー サイズ</strong></p></td>
<td align="left"><p>サポート技術情報内の各バッファーのサイズ。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>最大バッファー</strong></p></td>
<td align="left"><p>同時に使用されているバッファーの最大数。 使用して、 <strong>-最大</strong>この値を変更するパラメーター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>最小バッファー</strong></p></td>
<td align="left"><p>セッションに割り当てられたバッファーの最小数。 使用して、<strong>最小</strong>パラメーターがこの値を設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>バッファーの数</strong></p></td>
<td align="left"><p>実際に、セッションに割り当てられたバッファーの数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>空きバッファー</strong></p></td>
<td align="left"><p>バッファーが割り当てられますが、使用されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>書き込まれたバッファー</strong></p></td>
<td align="left"><p>トレース セッション中に書き込まれたバッファーの合計数。 値を超えることができますので、データの書き込みおよびフラッシュし、書き換え、バッファーが含まれます<strong>最大バッファー</strong>します。</p>
<p>連続したログ ファイルのサイズを推定するには、乗算<strong>バッファーが書き込まれる</strong>によって<strong>バッファー サイズ</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>イベントが失われました</strong></p></td>
<td align="left"><p>生成されたが記録されませんが、通常、すべての割り当てられたバッファーがいっぱいのためのイベントの数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ログ バッファーが失われる</strong></p></td>
<td align="left"><p>コンテンツを持つをログに書き込まれませんでしたバッファーの数。 通常、このエラーは、ログの内容を保持するために十分なディスク領域がない場合にのみ発生します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>リアルタイム バッファーが失われる</strong></p></td>
<td align="left"><p>コンテンツを配信できませんでしたバッファーの数。 通常、これは、システム リソースが不足しているときに発生します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>AgeLimit</strong></p></td>
<td align="left"><p>未使用のバッファーが解放される前に、の時間の遅延。 この値を変更するには使用<strong>-年齢</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>モード</em></p>
<p>(リアル タイム モードを有効に、ログ ファイルのモード、バッファリング モードのみ)</p></td>
<td align="left"><p>このセッションで有効になっているログ モードです。 ログ モード定数の完全な一覧は、Windows SDK のドキュメントを参照してください。</p>
<div class="alert">
<strong>注:</strong><br/><p><strong>ログ ファイル モード</strong>とログ ファイルが書き込まれていないエントリにも表示されます。 ログ ファイルの形式が表示されます。</p>
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td align="left"><p><strong>トレースを有効になっています。</strong></p></td>
<td align="left"><p>トレースする NT Kernel Logger イベント。 このフィールドは、NT Kernel Logger セッションをトレースする場合にのみ表示されます。</p>
<div class="alert">
<strong>注:</strong><br/><p>このフィールドには、トレースする場合でも、DPC、ISR、およびコンテキストの切り替えイベントは表示されません。</p>
</div>
<div>

</div></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ログ ファイル名</strong></p></td>
<td align="left"><p>ログ ファイルは、セッションに使用します。 リアルタイムおよびバッファー内のトレース セッションでは、フィールドの値は空白です。</p>
<p>この値を変更するには使用<strong>-f</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>使用中のローカル/グローバル シーケンス番号。</strong></p></td>
<td align="left"><p>ローカルまたはグローバルのシーケンス番号が使用される場合のみが表示されます。</p>
<p>このプロパティを変更するには使用<strong>ls</strong>または<strong>-gs</strong>します。</p></td>
</tr>
</tbody>
</table>
