---
title: KSPROPERTY\_クロック\_FUNCTIONTABLE
description: クライアントの使用、KSPROPERTY\_クロック\_FUNCTIONTABLE プロパティ ディスパッチ時刻を照会するためのエントリ ポイントを取得する\_により、正確な速度の一致を実行するためのフィルターのレベル。
ms.assetid: 6dac5688-fd69-416c-a4e4-da9ccc45c32a
keywords:
- KSPROPERTY_CLOCK_FUNCTIONTABLE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CLOCK_FUNCTIONTABLE
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c6bacea3a80de97e5d6ac60f0f33a1177303723
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342810"
---
# <a name="kspropertyclockfunctiontable"></a>KSPROPERTY\_クロック\_FUNCTIONTABLE


クライアントの使用、KSPROPERTY\_クロック\_FUNCTIONTABLE プロパティ ディスパッチ時刻を照会するためのエントリ ポイントを取得する\_により、正確な速度の一致を実行するためのフィルターのレベル。 このプロパティを設定、 [ **KSCLOCK\_FUNCTIONTABLE** ](https://msdn.microsoft.com/library/windows/hardware/ff561020)時計が解放されるに、ファイル オブジェクトまで有効な関数ポインターを含む構造体。

## <span id="ddk_ksproperty_clock_functiontable_ks"></span><span id="DDK_KSPROPERTY_CLOCK_FUNCTIONTABLE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561020" data-raw-source="[&lt;strong&gt;KSCLOCK_FUNCTIONTABLE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561020)"><strong>KSCLOCK_FUNCTIONTABLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

*FileObject*これらのエントリ ポイントへの呼び出しを行うときに、クライアントが提供するパラメーターは、クロックのインスタンスが作成されたときに返されたファイル ハンドルを基になるファイル オブジェクトを指定します。

*SystemTime*パラメーター相関のシステム時刻を格納する場所を指します。 システム時刻は、関数を使用して取得した**KeQueryInterruptTime**します。

参照してください[KS クロック](https://msdn.microsoft.com/library/windows/hardware/ff567307)します。

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


[**KSCLOCK\_FUNCTIONTABLE**](https://msdn.microsoft.com/library/windows/hardware/ff561020)

[**KeQueryInterruptTime**](https://msdn.microsoft.com/library/windows/hardware/ff553025)

 

 






