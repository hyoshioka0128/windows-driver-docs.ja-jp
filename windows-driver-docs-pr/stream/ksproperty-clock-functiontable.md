---
title: KSK プロパティ\_CLOCK\_FUNCTIONTABLE
description: クライアントは、KSK プロパティ\_CLOCK\_FUNCTIONTABLE プロパティを使用して、ディスパッチ\_レベルで時間をクエリするためのエントリポイントを取得します。これにより、フィルターは正確なレート一致を実行できます。
ms.assetid: 6dac5688-fd69-416c-a4e4-da9ccc45c32a
keywords:
- KSPROPERTY_CLOCK_FUNCTIONTABLE ストリーミングメディアデバイス
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
ms.openlocfilehash: b15fe10a798fb8b19e56f4c83036238d353c2506
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826899"
---
# <a name="ksproperty_clock_functiontable"></a>KSK プロパティ\_CLOCK\_FUNCTIONTABLE


クライアントは、KSK プロパティ\_CLOCK\_FUNCTIONTABLE プロパティを使用して、ディスパッチ\_レベルで時間をクエリするためのエントリポイントを取得します。これにより、フィルターは正確なレート一致を実行できます。 このプロパティは、クロックのファイルオブジェクトが解放されるまで有効な関数ポインターを使用して、 [**Ksclock\_FUNCTIONTABLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksclock_functiontable)構造体に格納します。

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
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>必須ではない</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksclock_functiontable" data-raw-source="[&lt;strong&gt;KSCLOCK_FUNCTIONTABLE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksclock_functiontable)"><strong>KSCLOCK_FUNCTIONTABLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

これらのエントリポイントを呼び出すときにクライアントが提供する*FileObject*パラメーターは、クロックインスタンスの作成時に返されたファイルハンドルの基になるファイルオブジェクトを指定します。

*SystemTime*パラメーターは、相関システム時刻を格納する場所を指します。 システム時刻は、関数**KeQueryInterruptTime**を使用して取得されます。

「 [KS クロック](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-clocks)」も参照してください。

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


[**関数テーブル\_KSCLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksclock_functiontable)

[**KeQueryInterruptTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequeryinterrupttime)

 

 






