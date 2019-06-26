---
title: KSPROPERTY\_接続\_状態
description: KSPROPERTY\_接続\_状態プロパティが現在の実行、暗証番号 (pin) の状態を設定します。
ms.assetid: f1a9e101-1398-4f16-bae9-f827e7d0c433
keywords:
- KSPROPERTY_CONNECTION_STATE ストリーミング メディア デバイス
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
ms.openlocfilehash: 1236346cc9da2e37cba9f6c3b0e624450ebab6c3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373107"
---
# <a name="kspropertyconnectionstate"></a>KSPROPERTY\_接続\_状態


KSPROPERTY\_接続\_状態プロパティが現在の実行、暗証番号 (pin) の状態を設定します。

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
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>フィルターまたはピン留めします。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ne-ks-ksstate" data-raw-source="[&lt;strong&gt;KSSTATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ne-ks-ksstate)"><strong>KSSTATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、次の値のいずれかを返します。

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
<td><p>Pin の初期状態です。 データが実際のない読み取りまたは書き込み。 この状態では、pin は、最小限のリソースをできる限りを使用します。</p></td>
</tr>
<tr class="even">
<td><p>KSSTATE_ACQUIRE</p></td>
<td><p>Pin はデータの読み書きに必要なリソースを取得しています。</p></td>
</tr>
<tr class="odd">
<td><p>KSSTATE_PAUSE</p></td>
<td><p>Pin はデータを読み取ったり書き込んだりする準備が、データ転送が一時的に停止されました。</p></td>
</tr>
<tr class="even">
<td><p>KSSTATE_RUN</p></td>
<td><p>元のピン留めする、実際の読み取りまたは書き込みデータの状態。</p></td>
</tr>
</tbody>
</table>

 

のみ、暗証番号 (pin) の読み取りまたはデータを書き込み、 **KSSTATE\_実行**状態。 個々 のピンと、KS の両方をフィルター処理全体は、このプロパティをサポート可能性があります。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ne-ks-ksstate)

 

 






