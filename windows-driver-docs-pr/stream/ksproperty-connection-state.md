---
title: KSK プロパティ\_接続\_の状態
description: KSK プロパティ\_CONNECTION\_STATE プロパティは、pin の現在の実行状態を設定します。
ms.assetid: f1a9e101-1398-4f16-bae9-f827e7d0c433
keywords:
- KSPROPERTY_CONNECTION_STATE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CONNECTION_STATE
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 187e78a7790a128fa975bacc15ad5a552c3660f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826780"
---
# <a name="ksproperty_connection_state"></a>KSK プロパティ\_接続\_の状態


KSK プロパティ\_CONNECTION\_STATE プロパティは、pin の現在の実行状態を設定します。

## <span id="ddk_ksproperty_connection_state_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_STATE_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>フィルターまたはピン留め</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-ksstate" data-raw-source="[&lt;strong&gt;KSSTATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-ksstate)"><strong>KSSTATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、次のいずれかの値を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KSSTATE_STOP</p></td>
<td><p>Pin の初期状態。 実際に読み取りまたは書き込みが行われているデータはありません。 この状態では、pin が使用できるリソースの量が最小限に抑えられます。</p></td>
</tr>
<tr class="even">
<td><p>KSSTATE_ACQUIRE</p></td>
<td><p>Pin は、データの読み取りまたは書き込みに必要なリソースを取得しています。</p></td>
</tr>
<tr class="odd">
<td><p>KSSTATE_PAUSE</p></td>
<td><p>Pin はデータの読み取りまたは書き込みの準備ができていますが、データ転送は一時的に一時停止されています。</p></td>
</tr>
<tr class="even">
<td><p>KSSTATE_RUN</p></td>
<td><p>Pin が実際にデータを読み取ったり書き込んだりできる状態。</p></td>
</tr>
</tbody>
</table>

 

Pin は、 **Ksk 状態\_実行**状態のデータの読み取りまたは書き込みのみを行います。 個々のピンと KS フィルターが全体として、このプロパティをサポートする場合があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ks (Ks を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-ksstate)

 

 






