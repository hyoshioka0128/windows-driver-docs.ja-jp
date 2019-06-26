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
ms.openlocfilehash: 32b71dc49caeb92730c33e6265d71288e0ce475c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373145"
---
# <a name="kspropertyclockfunctiontable"></a>KSPROPERTY\_クロック\_FUNCTIONTABLE


クライアントの使用、KSPROPERTY\_クロック\_FUNCTIONTABLE プロパティ ディスパッチ時刻を照会するためのエントリ ポイントを取得する\_により、正確な速度の一致を実行するためのフィルターのレベル。 このプロパティを設定、 [ **KSCLOCK\_FUNCTIONTABLE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksclock_functiontable)時計が解放されるに、ファイル オブジェクトまで有効な関数ポインターを含む構造体。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksclock_functiontable" data-raw-source="[&lt;strong&gt;KSCLOCK_FUNCTIONTABLE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksclock_functiontable)"><strong>KSCLOCK_FUNCTIONTABLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

*FileObject*これらのエントリ ポイントへの呼び出しを行うときに、クライアントが提供するパラメーターは、クロックのインスタンスが作成されたときに返されたファイル ハンドルを基になるファイル オブジェクトを指定します。

*SystemTime*パラメーター相関のシステム時刻を格納する場所を指します。 システム時刻は、関数を使用して取得した**KeQueryInterruptTime**します。

参照してください[KS クロック](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-clocks)します。

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


[**KSCLOCK\_FUNCTIONTABLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksclock_functiontable)

[**KeQueryInterruptTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kequeryinterrupttime)

 

 






