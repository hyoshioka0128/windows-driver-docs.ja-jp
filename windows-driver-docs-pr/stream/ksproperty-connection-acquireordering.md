---
title: KSPROPERTY\_接続\_ACQUIREORDERING
description: KSPROPERTY\_接続\_ACQUIREORDERING プロパティが省略可能なプロパティと状態変更の順序は重要では pin 上に実装する必要があります。
ms.assetid: b0d27615-bece-49b1-8497-f3c389ea37fc
keywords:
- KSPROPERTY_CONNECTION_ACQUIREORDERING ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CONNECTION_ACQUIREORDERING
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: efe4be575e6a2b8ece4d5223a44bfc6b0be5d7cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571053"
---
# <a name="kspropertyconnectionacquireordering"></a>KSPROPERTY\_接続\_ACQUIREORDERING


KSPROPERTY\_接続\_ACQUIREORDERING プロパティが省略可能なプロパティと状態変更の順序は重要では pin 上に実装する必要があります。 たとえば、シンクはシンクのピンを設定する前に取得状態に設定する、通信ソース ピンに接続して pin を必要とする場合、通信シンク ピンのプロパティを実装する必要があります。

## <span id="ddk_ksproperty_connection_acquireordering_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_ACQUIREORDERING_KS"></span>


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
<th>Set</th>
<th>移行先</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

このプロパティを返します**TRUE**状態変更の順序が重要な場合。 場合**FALSE**を返すプロパティを実装しない必要があります。

この読み取り専用プロパティは取得停止状態の変更がこの通信のシンクの pin の重要なかどうかを判断するために使用します。 プロパティが実装されていない場合、前提は、こと順序重要です。 IRP ベースのデータ フローでは、これは実装されます pin 要求の場合、新しい作成の Irp ではなくストリーミング Irp を転送し、接続されたソースの暗証番号 (pin) を適切なスタックの深さを示す必要がある場合。 Pin は Irp を転送しませんが場合、し、スタックの深さの再計算はできません、重要なフィルターのスタックの深さが静的とします。

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


[KSPROPSETID\_接続](kspropsetid-connection.md)

 

 






