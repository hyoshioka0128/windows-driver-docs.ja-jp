---
title: WDI_TLV_DATAPATH_CAPABILITIES
description: WDI_TLV_DATAPATH_CAPABILITIES は、データパス機能を含む TLV です。
ms.assetid: 7B545858-56A2-4655-91D5-37CA4EB61E1E
ms.date: 07/18/2017
keywords:
- WDI_TLV_DATAPATH_CAPABILITIES ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 2120ebfc5bf9fc9d93ae75f0e4a97eae3ca40598
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844501"
---
# <a name="wdi_tlv_datapath_capabilities"></a>WDI\_TLV\_データパス\_の機能


WDI\_TLV\_データパス\_機能は、データパス機能を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0xB9

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>タスクバーの検索ボックスに</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ne-dot11wdi-_wdi_interconnect_type" data-raw-source="[&lt;strong&gt;WDI_INTERCONNECT_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ne-dot11wdi-_wdi_interconnect_type)"><strong>WDI_INTERCONNECT_TYPE</strong></a> (UINT32)</td>
<td>相互接続の種類。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>ピアの最大数。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>送信機能を指定します: 対象優先順位キュー。
<p>有効な値は0と1です。 0に設定すると、WDI はピアと TID によって Tx フレームを分類し、完全なスケジューラを利用して転送する TX キューを選択します。 ターゲットが分類およびピア TID キューに対応している場合を除き、この値を false に設定することをお勧めします。 1に設定すると、WDI はピアと TID によって Tx フレームを分類し、ポートレベルでのみキューを提供します。 WDI は、グローバル DRR を使用してバックログのポートキューをスケジュールします。</p></td>
</tr>
<tr class="even">
<td>UINT16</td>
<td>送信機能を指定します。フレーム内のスキャッター Gather 要素の最大数です。
<p>WDI は、必要に応じてフレームを結合します。これにより、IHV ミニポートは、この機能で指定されているよりも多くのスキャッター収集要素を必要とするフレームを受信しません。 最適なパフォーマンスを得るには、合体にメモリコピーが必要になるため、この機能が一般的なフレームよりも高い値に設定されていることをお勧めします。 この機能が、ページサイズで割った最大フレームサイズを超えていない場合、WDI はフレームを結合できず、削除される可能性があります。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>送信機能を指定します: Explicit Send Complete フラグが必要です。
<p>有効な値は0と1です。 0に設定すると、ターゲット/TAL はすべてのフレームに対して TX 送信の完了を生成します。 1に設定すると、ターゲット/TAL は、フレームのメタデータにこのフラグが設定されているフレームに対してのみ TX 送信の完了を示す値を生成します。</p></td>
</tr>
<tr class="even">
<td>UINT16</td>
<td>送信機能を指定します: 最小有効フレームサイズ。
<p>フレームをデキューするときに、TxMgr はこの値より小さいフレームをこの値の有効なサイズとして扱います。</p></td>
</tr>
<tr class="odd">
<td>UINT16</td>
<td>送信機能を指定します。フレームサイズの粒度です。
<p>この値は、フレームごとのメモリ割り当ての粒度と同じです。 デキューの目的では、TxMgr はフレームをフレームサイズと同じ大きさにして、有効なサイズがこの値の整数倍数であるように最小の余白を加えたものとして扱います。 この値は2の累乗に設定する必要があります。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>送信機能を指定します: Rx Tx 転送。
<p>有効な値は0と1です。 1に設定すると、ターゲットは受信したフレームを転送できるようになります。</p></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>送信機能: 最大スループットを 0.5 Mbps 単位で指定します。
<p>この値は、記述子とバッファーの割り当てに使用されます。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 




