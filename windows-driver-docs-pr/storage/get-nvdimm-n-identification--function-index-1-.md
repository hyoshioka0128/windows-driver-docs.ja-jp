---
title: NVDIMM-N ID の取得 (関数インデックス 1)
description: この関数は、デバイスに固有の情報を返します。
ms.assetid: 350E764D-634C-4C60-9C74-E26B01636C02
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e3398aa1e52831e03496f7f850715362bba5a2ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360914"
---
# <a name="span-idstoragegetnvdimm-nidentificationfunctionindex1spanget-nvdimm-n-identification-function-index-1"></a><span id="storage.get_nvdimm-n_identification__function_index_1_"></span>NVDIMM-N 識別 (関数インデックス 1) を取得します。


この関数は、デバイスに固有の情報を返します。

&gt; \[!注\]    &gt;、星が付いたマークされているすべてのレジスタ (\*) バイト アドレス指定可能なエネルギー バックアップ インターフェイス仕様で定義されているレジスタします。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>入力


### <a name="span-idarg3spanspan-idarg3spanspan-idarg3spanarg3"></a><span id="Arg3"></span><span id="arg3"></span><span id="ARG3"></span>arg3…

なし。

## <a name="span-idoutputspanspan-idoutputspanspan-idoutputspanoutput"></a><span id="Output"></span><span id="output"></span><span id="OUTPUT"></span>出力


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド</th>
<th align="left">バイトの長さ</th>
<th align="left">バイト オフセット</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>ステータス</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>移動して<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>について。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>仕様のリビジョン</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>モジュールでサポートされている仕様バージョン。</p>
<p><em>バイト 0 – <em>SPECREV</em>このレジスタに 1 バイトのアドレス指定可能なエネルギー バックアップ インターフェイスを登録しますが (0, 0x06)。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>標準的なページ数</strong></td>
<td align="left">1</td>
<td align="left">5</td>
<td align="left"><p>モジュールでサポートされている標準の定義ページの数。</p>
<p></em>Byte 0 – <em>STD_NUM_PAGES</em> (0, 0x01)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>仕入先の最初のページ</strong></td>
<td align="left">1</td>
<td align="left">6</td>
<td align="left"><p>ベンダー固有のページの開始ページ番号。</p>
<p><em>バイト 0 – <em>VENDOR_START_PAGES</em> (0, 0x02)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>仕入先ページの数</strong></td>
<td align="left">1</td>
<td align="left">7</td>
<td align="left"><p>モジュールでサポートされているベンダー固有のページの数。</p>
<p></em>バイト 0 – <em>VENDOR_NUM_PAGES</em> (0, 0x03)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ハードウェアのリビジョン</strong></td>
<td align="left">4</td>
<td align="left">8</td>
<td align="left"><p>コント ローラー ハードウェア リビジョン。</p>
<p><em>バイト 0 – <em>HWREV</em> (0, 0x04)</p>
<p>1 - バイトに予約されています。</p>
<p>2 - バイトに予約されています。</p>
<p>3 - バイトに予約されています。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ファームウェアのリビジョン</strong></td>
<td align="left">2</td>
<td align="left">12</td>
<td align="left"><p>アクティブなファームウェア スロットのファームウェアのバージョン。</p>
<p></em>バイト 0 – <em>SLOTX_FWREV0</em> (0, 0x07/0x09)</p>
<p><em>1 – バイト<em>SLOTX_FWREV1</em> (0, 0x08/0x0A)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>現在のファームウェア スロット</strong></td>
<td align="left">1</td>
<td align="left">14</td>
<td align="left"><p>実行中のファームウェア イメージのスロットの数。</p>
<p></em>バイト 0 ~ 7:4 ビット<em>FW_SLOT_INFO</em> (3, 0x42) の登録 (<em>RUNNING_FW_SLOT</em>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ファームウェア スロット数</strong></td>
<td align="left">1</td>
<td align="left">15</td>
<td align="left"><p>利用可能なファームウェア スロットの数。 JEDEC 準拠デバイスの場合は、このフィールドを 2 となります。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>機能</strong></td>
<td align="left">1</td>
<td align="left">16</td>
<td align="left"><p>モジュールでサポートされる機能に関する情報です。</p>
<p><em>バイト 0 –<em>機能</em>(0, 0x10)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>サポートされているバックアップのトリガー</strong></td>
<td align="left">1</td>
<td align="left">17</td>
<td align="left"><p>モジュールのサポートされているは、トリガーを保存します。</p>
<p></em>バイト 0 – <em>CSAVE_TRIGGER_SUPPORT</em> (0, 0x16)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>操作の最大再試行回数</strong></td>
<td align="left">1</td>
<td align="left">18</td>
<td align="left"><p>推奨されるは、ホストの数を再試行してください、保存、復元または消去する操作が失敗した場合か、タイムアウトの最大値を超えています。</p>
<p><em>Byte 0 – <em>HOST_MAX_OPERATION_RETRY</em> (0, 0x15)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>サポートされている通知イベント</strong></td>
<td align="left">1</td>
<td align="left">19</td>
<td align="left"><p>モジュールのイベント情報の通知が生成されます。</p>
<p></em>バイト 0 – <em>EVENT_NOTIFICATION_SUPPORT</em> (0, 0x17)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>保存操作のタイムアウト</strong></td>
<td align="left">4</td>
<td align="left">20</td>
<td align="left"><p>最悪の場合は、ミリ秒または秒で完了の待機時間を保存します。</p>
<p><em>Byte 0 – <em>CSAVE_TIMEOUT0</em> (0, 0x18)</p>
<p></em>1 – バイト<em>CSAVE_TIMEOUT1</em> (0, 0x19)</p>
<p>2 - バイトに予約されています。</p>
<p>3 - バイトに予約されています。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>復元操作のタイムアウト</strong></td>
<td align="left">4</td>
<td align="left">24</td>
<td align="left"><p>最悪の場合は、完了の待機時間のミリ秒または秒を復元します。</p>
<p><em>バイト 0 – <em>RESTORE_TIMEOUT0</em> (0, 0x1C)</p>
<p></em>1 – バイト<em>RESTORE_TIMEOUT1</em> (0, 0x1D)</p>
<p>2 - バイトに予約されています。</p>
<p>3 - バイトに予約されています。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>操作のタイムアウトを消去します。</strong></td>
<td align="left">4</td>
<td align="left">28</td>
<td align="left"><p>最悪の場合は、完了の待機時間のミリ秒または秒を消去します。</p>
<p><em>バイト 0 – <em>ERASE_TIMEOUT0</em> (0, 0x1E)</p>
<p></em>1 – バイト<em>ERASE_TIMEOUT1</em> (0, 0x1F)</p>
<p>2 - バイトに予約されています。</p>
<p>3 - バイトに予約されています。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>Arm 操作のタイムアウト</strong></td>
<td align="left">4</td>
<td align="left">32</td>
<td align="left"><p>ミリ秒または秒単位で最悪のケースの arm 完了待ち時間。</p>
<p>Byte 0 – <em>ARM_TIMEOUT0</em> (0, 0x20)</p>
<p>1 – バイト<em>ARM_TIMEOUT1</em> (0, 0x21)</p>
<p>2 - バイトに予約されています。</p>
<p>3 - バイトに予約されています。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ファームウェア操作のタイムアウト</strong></td>
<td align="left">4</td>
<td align="left">36</td>
<td align="left"><p>最悪大文字と小文字のファームウェア操作完了の遅延にミリ秒または秒。</p>
<p><em>バイト 0 – <em>FIRMWARE_OPS_TIMEOUT0</em> (0, 0x22)</p>
<p></em>1 – バイト<em>FIRMWARE_OPS_TIMEOUT1</em> (0, 0x23)</p>
<p>2 - バイトに予約されています。</p>
<p>3 - バイトに予約されています。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>中止操作のタイムアウト</strong></td>
<td align="left">4</td>
<td align="left">40</td>
<td align="left"><p></p>
<p><em>バイト 0 – <em>ABORT_CMD_TIMEOUT0</em> (0, 0x24)</p>
<p>1 – バイトに予約されています。</p>
<p>2 - バイトに予約されています。</p>
<p>3 - バイトに予約されています。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>最小の動作温度</strong></td>
<td align="left">1</td>
<td align="left">44</td>
<td align="left"><p>温度を摂氏で最小値。</p>
<p></em>バイト 0 – <em>MIN_OPERATING_TEMP</em> (0, 0x25)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>最大操作温度</strong></td>
<td align="left">1</td>
<td align="left">45</td>
<td align="left"><p>温度を摂氏で最大です。</p>
<p><em>バイト 0 – <em>MAX_OPERATING_TEMP</em> (0, 0x26)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>リージョンのブロック サイズ</strong></td>
<td align="left">4</td>
<td align="left">46</td>
<td align="left"><p>32 バイトの倍数単位の領域のサイズ。</p>
<p></em>バイト 0 – <em>REGION_BLOCK_SIZE</em> (0, 0x32)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






