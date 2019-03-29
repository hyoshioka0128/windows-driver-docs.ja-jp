---
title: KSPROPERTY\_PIN\_データ フロー
description: KSPROPERTY\_PIN\_データフロー プロパティ pin ファクトリによってインスタンス化するピンのデータ フローの方向を指定します。 シンクのピンは、フィルターのエントリ ポイントです。フィルターからソース ピンの出力。
ms.assetid: 3132b344-c4f3-48dc-9829-f4e97d0f18fc
keywords:
- KSPROPERTY_PIN_DATAFLOW ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_DATAFLOW
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15816fbe2f46c844b8185fe23463ea8a718d786e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580208"
---
# <a name="kspropertypindataflow"></a>KSPROPERTY\_PIN\_データ フロー


KSPROPERTY\_PIN\_データフロー プロパティ pin ファクトリによってインスタンス化するピンのデータ フローの方向を指定します。 シンクのピンは、フィルターのエントリ ポイントです。フィルターからソース ピンの出力。

## <span id="ddk_ksproperty_pin_dataflow_ks"></span><span id="DDK_KSPROPERTY_PIN_DATAFLOW_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566722)"><strong>KSP_PIN</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563532" data-raw-source="[&lt;strong&gt;KSPIN_DATAFLOW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563532)"><strong>KSPIN_DATAFLOW</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

ピン留めするファクトリを指定、 **PinId**のメンバー、 [ **KSP\_PIN** ](https://msdn.microsoft.com/library/windows/hardware/ff566722)構造体。

KSPROPERTY\_PIN\_データ フローは、型の列挙体を返します[ **KSPIN\_データフロー**](https://msdn.microsoft.com/library/windows/hardware/ff563532)、いずれかに設定**KSPIN\_データ フロー\_IN**または KSPIN\_データフロー\_アウトします。

Stream ミニドライバーは、このプロパティを直接処理する必要はありません。ストリーム クラス ドライバーは、ストリーム要求のブロックを使用して詳細情報を照会するこのプロパティを処理します。

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


[**KSP\_暗証番号 (PIN)**](https://msdn.microsoft.com/library/windows/hardware/ff566722)

[**KSPIN\_データ フロー**](https://msdn.microsoft.com/library/windows/hardware/ff563532)

 

 






