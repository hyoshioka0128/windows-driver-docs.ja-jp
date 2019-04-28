---
title: KSPROPERTY\_PIN\_NECESSARYINSTANCES
description: このプロパティは、pin の最小数を返します、暗証番号 (pin) ファクトリは、フィルターが I/O 操作を実行する前にインスタンス化する必要があります。
ms.assetid: d30d7546-3d16-42df-b640-a8ec37bca35c
keywords:
- KSPROPERTY_PIN_NECESSARYINSTANCES ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_NECESSARYINSTANCES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e1cb63bedb92457f4dec24ec35aace06c4a1b5c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380813"
---
# <a name="kspropertypinnecessaryinstances"></a>KSPROPERTY\_PIN\_NECESSARYINSTANCES


このプロパティは、pin の最小数を返します、暗証番号 (pin) ファクトリは、フィルターが I/O 操作を実行する前にインスタンス化する必要があります。

## <span id="ddk_ksproperty_pin_necessaryinstances_ks"></span><span id="DDK_KSPROPERTY_PIN_NECESSARYINSTANCES_KS"></span>


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
<td><p>〇</p></td>
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566722)"><strong>KSP_PIN</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSP を使用してこのプロパティを指定\_暗証番号 (pin)、メンバーが、関連する pin ファクトリを指定します。

KSPROPERTY\_PIN\_NECESSARYINSTANCES がピン留めするファクトリのインスタンスを作成する必要があります pin の最小数を指定する ULONG 型の値を返します。

クラス ドライバーは、このプロパティを処理しませんストリームのミニドライバーは、独自の処理を提供する必要があります。

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
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_暗証番号 (PIN)**](https://msdn.microsoft.com/library/windows/hardware/ff566722)

 

 






