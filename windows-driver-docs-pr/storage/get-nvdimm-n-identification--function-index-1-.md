---
title: NVDIMM-N ID の取得 (関数インデックス 1)
description: この関数は、デバイス固有の情報を返します。
ms.assetid: 350E764D-634C-4C60-9C74-E26B01636C02
ms.localizationpriority: medium
ms.date: 01/08/2020
ms.openlocfilehash: edf3c46cf2dcef50c1b1444836d3982c04114a00
ms.sourcegitcommit: 3fbf71b2bd92abca0bfb3c373f57af9a0eb67c93
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/09/2020
ms.locfileid: "75780848"
---
# <a name="get-nvdimm-n-identification-function-index-1"></a>NVDIMM-N ID の取得 (関数インデックス 1)

この関数は、デバイス固有の情報を返します。

> [!NOTE]
> スター (\*) でマークされたすべてのレジスタは、バイトアドレッシング可能なエネルギーバッキングインターフェイスの仕様で定義されているレジスタです。

## <a name="input"></a>入力

### <a name="arg3"></a>Arg3

なし。

## <a name="output"></a>出力

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
<th align="left">バイト長</th>
<th align="left">バイト オフセット</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>状態</strong></td>
<td align="left">ホーム フォルダーが置かれているコンピューターにアクセスできない</td>
<td align="left">0</td>
<td align="left"><p>詳細については、 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>にアクセスしてください。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>仕様のリビジョン</strong></td>
<td align="left">1 で保護されたプロセスとして起動されました</td>
<td align="left">ホーム フォルダーが置かれているコンピューターにアクセスできない</td>
<td align="left"><p>モジュールでサポートされている仕様のバージョン。</p>
<p>バイト0– <em>Specrev</em> (0, 0X06) このレジスタは、バイトアドレッシング可能なエネルギーサポートインターフェイスレジスタです。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>標準ページ数</strong></td>
<td align="left">1 で保護されたプロセスとして起動されました</td>
<td align="left">5</td>
<td align="left"><p>モジュールでサポートされている標準の定義ページの数。</p>
<p>バイト0– <em>STD_NUM_PAGES</em> (0, 0x01)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>最初のベンダページ</strong></td>
<td align="left">1 で保護されたプロセスとして起動されました</td>
<td align="left">6</td>
<td align="left"><p>ベンダー固有のページの開始ページ番号。</p>
<p>バイト0– <em>VENDOR_START_PAGES</em> (0, 0x02)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ベンダーのページ数</strong></td>
<td align="left">1 で保護されたプロセスとして起動されました</td>
<td align="left">7</td>
<td align="left"><p>モジュールでサポートされているベンダー固有のページの数。</p>
<p>バイト0– <em>VENDOR_NUM_PAGES</em> (0, 0x03)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ハードウェアのリビジョン</strong></td>
<td align="left">ホーム フォルダーが置かれているコンピューターにアクセスできない</td>
<td align="left">8</td>
<td align="left"><p>コントローラーのハードウェアリビジョン。</p>
<p>バイト0– <em>HWREV</em> (0, 0x04)</p>
<p>バイト 1-予約済み。</p>
<p>バイト 2-予約済み。</p>
<p>バイト 3-予約済み。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ファームウェアのリビジョン</strong></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">12</td>
<td align="left"><p>アクティブなファームウェアスロットのファームウェアバージョン。</p>
<p>バイト0– <em>SLOTX_FWREV0</em> (0, 0x07/0x09)</p>
<p>バイト1– <em>SLOTX_FWREV1</em> (0、0X08/0x0a)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>現在のファームウェアスロット</strong></td>
<td align="left">1 で保護されたプロセスとして起動されました</td>
<td align="left">14</td>
<td align="left"><p>実行中のファームウェアイメージのスロット番号。</p>
<p><em>FW_SLOT_INFO</em> (3、0x42) レジスタ (<em>RUNNING_FW_SLOT</em>) のバイト0–ビット [7:4]。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ファームウェアのスロット数</strong></td>
<td align="left">1 で保護されたプロセスとして起動されました</td>
<td align="left">15</td>
<td align="left"><p>使用可能なファームウェアスロットの数。 JEDEC に準拠しているデバイスの場合、このフィールドは2にする必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>機能</strong></td>
<td align="left">1 で保護されたプロセスとして起動されました</td>
<td align="left">16</td>
<td align="left"><p>モジュールでサポートされている機能に関する情報。</p>
<p>バイト0– <em>CAPABILITIES0</em> (0, 0x10)</p>
<p>Byte 1 – <em>CAPABILITIES1</em> (0, 0x11)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>サポートされているバックアップトリガー</strong></td>
<td align="left">1 で保護されたプロセスとして起動されました</td>
<td align="left">17</td>
<td align="left"><p>モジュールでサポートされている保存トリガー。</p>
<p></em>バイト0– <em>CSAVE_TRIGGER_SUPPORT</em> (0, 0x16)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>操作の最大再試行回数</strong></td>
<td align="left">1 で保護されたプロセスとして起動されました</td>
<td align="left">18</td>
<td align="left"><p>保存、復元、または消去操作が失敗した場合、または最大タイムアウト値を超えた場合に、ホストに推奨される再試行回数。</p>
<p>バイト0– <em>HOST_MAX_OPERATION_RETRY</em> (0, 0x15)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>サポートされている通知イベント</strong></td>
<td align="left">1 で保護されたプロセスとして起動されました</td>
<td align="left">19</td>
<td align="left"><p>モジュールが通知を生成するイベント情報。</p>
<p>バイト0– <em>EVENT_NOTIFICATION_SUPPORT</em> (0、0x17)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>保存操作のタイムアウト</strong></td>
<td align="left">ホーム フォルダーが置かれているコンピューターにアクセスできない</td>
<td align="left">20</td>
<td align="left"><p>最悪の場合は、完了までの待機時間をミリ秒または秒で節約できます。</p>
<p>バイト0– <em>CSAVE_TIMEOUT0</em> (0, 0x18)</p>
<p>バイト1– <em>CSAVE_TIMEOUT1</em> (0, 0x19)</p>
<p>バイト 2-予約済み。</p>
<p>バイト 3-予約済み。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>復元操作のタイムアウト</strong></td>
<td align="left">ホーム フォルダーが置かれているコンピューターにアクセスできない</td>
<td align="left">24</td>
<td align="left"><p>最悪の場合、復元完了までの待機時間 (ミリ秒または秒単位)。</p>
<p>バイト0– <em>RESTORE_TIMEOUT0</em> (0、0x1c)</p>
<p>バイト1– <em>RESTORE_TIMEOUT1</em> (0, 0x1d)</p>
<p>バイト 2-予約済み。</p>
<p>バイト 3-予約済み。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>消去操作のタイムアウト</strong></td>
<td align="left">ホーム フォルダーが置かれているコンピューターにアクセスできない</td>
<td align="left">28</td>
<td align="left"><p>最悪のケースでは、完了までの待機時間をミリ秒または秒で消去します。</p>
<p>バイト0– <em>ERASE_TIMEOUT0</em> (0, 0x1e)</p>
<p>バイト1– <em>ERASE_TIMEOUT1</em> (0, 0x1f)</p>
<p>バイト 2-予約済み。</p>
<p>バイト 3-予約済み。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>Arm 操作のタイムアウト</strong></td>
<td align="left">ホーム フォルダーが置かれているコンピューターにアクセスできない</td>
<td align="left">32</td>
<td align="left"><p>最悪の場合の arm 完了待機時間 (ミリ秒または秒)。</p>
<p>バイト0– <em>ARM_TIMEOUT0</em> (0, 0x20)</p>
<p>バイト1– <em>ARM_TIMEOUT1</em> (0、0x21)</p>
<p>バイト 2-予約済み。</p>
<p>バイト 3-予約済み。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ファームウェア操作のタイムアウト</strong></td>
<td align="left">ホーム フォルダーが置かれているコンピューターにアクセスできない</td>
<td align="left">36</td>
<td align="left"><p>最悪の場合のファームウェア操作完了の待機時間 (ミリ秒または秒)。</p>
<p>バイト0– <em>FIRMWARE_OPS_TIMEOUT0</em> (0, 0x22)</p>
<p>バイト1– <em>FIRMWARE_OPS_TIMEOUT1</em> (0, 0x23)</p>
<p>バイト 2-予約済み。</p>
<p>バイト 3-予約済み。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>中止操作のタイムアウト</strong></td>
<td align="left">ホーム フォルダーが置かれているコンピューターにアクセスできない</td>
<td align="left">40</td>
<td align="left"><p></p>
<p>バイト0– <em>ABORT_CMD_TIMEOUT</em> (0, 0x24)</p>
<p>バイト1–予約済み。</p>
<p>バイト 2-予約済み。</p>
<p>バイト 3-予約済み。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>領域ブロックサイズ</strong></td>
<td align="left">ホーム フォルダーが置かれているコンピューターにアクセスできない</td>
<td align="left">46</td>
<td align="left"><p>32バイトの倍数での領域のサイズ。</p>
<p>バイト0– <em>REGION_BLOCK_SIZE</em> (0, 0x32)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>最小動作温度</strong></td>
<td align="left">1 で保護されたプロセスとして起動されました</td>
<td align="left">44</td>
<td align="left"><p>摂氏の最小動作温度。</p>
<p>バイト0– <em>MIN_OPERATING_TEMP0</em> (0、0x38)</p>
<p>バイト1– <em>MIN_OPERATING_TEMP1</em> (0, 0x39)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>最大操作温度</strong></td>
<td align="left">1 で保護されたプロセスとして起動されました</td>
<td align="left">45</td>
<td align="left"><p>摂氏の最大操作温度。</p>
<p>バイト0– <em>MAX_OPERATING_TEMP0</em> (0、0x3a)</p>
<p>バイト1– <em>MAX_OPERATING_TEMP1</em> (0、0x3b)</p></td>
</tr>
</tbody>
</table>

## <a name="related-topics"></a>関連トピック

[バイトアドレッシング可能なエネルギー対応関数クラスの \_DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)
