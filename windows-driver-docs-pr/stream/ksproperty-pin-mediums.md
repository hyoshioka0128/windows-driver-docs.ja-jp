---
title: KSPROPERTY\_PIN\_メディア
description: このプロパティは、ピンのピン留めする特定のファクトリによってインスタンス化でサポートされているメディアの一覧を返します。
ms.assetid: e92c7a3d-4f72-4818-9a26-0e82c20bdb4c
keywords:
- KSPROPERTY_PIN_MEDIUMS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_MEDIUMS
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5995b9f6224d259ea95034acbcc29907e20fa24
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380816"
---
# <a name="kspropertypinmediums"></a>KSPROPERTY\_PIN\_メディア


このプロパティは、ピンのピン留めする特定のファクトリによってインスタンス化でサポートされているメディアの一覧を返します。

## <span id="ddk_ksproperty_pin_mediums_ks"></span><span id="DDK_KSPROPERTY_PIN_MEDIUMS_KS"></span>


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
<td><p>A <a href="https://msdn.microsoft.com/library/windows/hardware/ff563441" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563441)"> <strong>KSMULTIPLE_ITEM</strong> </a>のシーケンスに続く構造<a href="https://msdn.microsoft.com/library/windows/hardware/ff563538" data-raw-source="[&lt;strong&gt;KSPIN_MEDIUM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563538)"> <strong>KSPIN_MEDIUM</strong> </a>構造体。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

クライアントでは、このプロパティを使用して、pin の pin ファクトリによってインスタンス化でサポートされているすべてのメディアの一覧を要求します。 クライアントは、ピンに接続するときに使用する実際のメディアを指定します。

KSP を使用してこのプロパティを指定\_暗証番号 (pin)、メンバーがメディアの一覧を返すためのファクトリを暗証番号 (pin) を指定します。

KSPROPERTY\_PIN\_メディアは、クラス ドライバーの優先順のメディアを返します。

Stream ミニドライバーは、このプロパティを直接処理する必要はありません。ストリーム クラス ドライバーは、ストリーム要求のブロックを使用して詳細情報を照会するこのプロパティを処理します。

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

[**KSMULTIPLE\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff563441)

[**KSPIN\_中**](https://msdn.microsoft.com/library/windows/hardware/ff563538)

 

 






