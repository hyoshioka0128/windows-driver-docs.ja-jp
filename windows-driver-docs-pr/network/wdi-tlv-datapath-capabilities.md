---
title: WDI_TLV_DATAPATH_CAPABILITIES
description: WDI_TLV_DATAPATH_CAPABILITIES は、データパス機能を含む TLV です。
ms.assetid: 7B545858-56A2-4655-91D5-37CA4EB61E1E
ms.date: 07/18/2017
keywords:
- WDI_TLV_DATAPATH_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5a86ae49462f2f44206155d7985f2bc3f9ef7537
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331835"
---
# <a name="wditlvdatapathcapabilities"></a>WDI\_TLV\_データパス\_機能


WDI\_TLV\_データパス\_機能はデータパス機能を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xB9

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926068" data-raw-source="[&lt;strong&gt;WDI_INTERCONNECT_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926068)"><strong>WDI_INTERCONNECT_TYPE</strong> </a> (UINT32)</td>
<td>型を相互接続です。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>ピアの最大数。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指定の機能を送信します。優先順位キューのターゲット。
<p>有効な値とは、0 および 1 です。 場合は 0、WDI に設定では、ピアして TID Tx フレームは、分類を転送する送信キューを選択します。 完全なスケジューラを使用します。 これが、ターゲットがの分類およびピア TID キューをサポートしない限り、false に設定されていることをお勧めします。 1、WDI に設定するは、ピアして TID Tx フレームをによって分類され、ポート レベルでキューを提供するだけ場合です。 WDI は、グローバル DRR を使用して、ポートのバックログ キューをスケジュールします。</p></td>
</tr>
<tr class="even">
<td>UINT16</td>
<td>指定の機能を送信します。フレームで収集散布図の要素の最大数。
<p>WDI は、IHV ミニポートは散布図の詳細については、この機能によって指定された数よりに要素を収集を必要とするフレームを受け取らないように、必要に応じて、フレームを連結します。 最適なパフォーマンスは、この機能に必要なメモリのコピーを結合一般的なフレームよりも高く設定することをお勧めします。 この機能が最大フレーム サイズがページ サイズで割った値より大きい、WDI が正常にフレームを結合することがない可能性がありますと破棄される可能性があります。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指定の機能を送信します。明示的な送信完了フラグが必要です。
<p>有効な値とは、0 および 1 です。 ターゲット/話して 0 に設定するには、すべてのフレームの完全な TX 送信が生成されます。 場合、 場合 1、ターゲット/話してに設定するには、このフラグがフレームのメタデータで設定されたフレームに対してのみ TX 送信完了を示す値が生成されます。</p></td>
</tr>
<tr class="even">
<td>UINT16</td>
<td>指定の機能を送信します。有効な最小のフレームのサイズ。
<p>フレームをデキューするにはときに、TxMgr として扱われますフレームこの値よりも小さい値のサイズが有効です。</p></td>
</tr>
<tr class="odd">
<td>UINT16</td>
<td>指定の機能を送信します。フレームのサイズの粒度。
<p>この値はフレームごとのメモリ割り当ての粒度です。 TxMgr が有効なサイズが整数に、フレームのサイズと余白の最小量と等しくする有効なサイズを持つものとしてフレームを扱うデキューのために、この値の倍数です。 この値は、2 の累乗に設定する必要があります。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定の機能を送信します。Rx Tx 転送します。
<p>有効な値とは、0 および 1 です。 転送を受信したフレームのできる 1 をターゲットに設定する場合に。</p></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定の機能を送信します。0.5 Mbps 単位での最大スループットです。
<p>この値は、記述子とバッファーの割り当てに使用されます。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>必要条件
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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




