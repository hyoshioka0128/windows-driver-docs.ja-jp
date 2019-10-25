---
title: KSK プロパティ\_DIRECTSOUND3DLISTENER\_BATCH
description: KSK プロパティ\_DIRECTSOUND3DLISTENER\_BATCH プロパティは、3D リスナーのバッチモード設定を指定します。
ms.assetid: 370191f8-e5a2-40f0-a979-c14cf7f44756
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_BATCH オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DLISTENER_BATCH
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d9f2bebb2701bb0825f44d4845538c330c828d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830801"
---
# <a name="ksproperty_directsound3dlistener_batch"></a>KSK プロパティ\_DIRECTSOUND3DLISTENER\_BATCH


KSK プロパティ\_DIRECTSOUND3DLISTENER\_BATCH プロパティは、3D リスナーのバッチモード設定を指定します。

## <span id="ddk_ksproperty_directsound3dlistener_batch_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_BATCH_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">[購入]</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[はい]</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>型</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) はブール型で、バッチモード設定を指定します。

-   このプロパティの値が**TRUE**の場合、ミニポートドライバーは、リスナーのプロパティおよび関連付けられているすべてのバッファープロパティへのすべての変更をキャッシュする必要があります。

-   値が**FALSE**の場合、リスナーのプロパティとバッファーのプロパティへの変更は直ちに有効になります。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_DIRECTSOUND3DLISTENER\_バッチプロパティ要求は正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティが**TRUE**から**FALSE**に遷移すると、ミニポートドライバーは、キャッシュされたすべてのプロパティを直ちに有効にする必要があります。 可能な場合は、キャッシュされたプロパティを同時に有効にする必要があります。

3D リスナーのバッチモード設定の詳細については、Microsoft Windows SDK のドキュメントの**IDirectSound3DListener:: CommitDeferredSettings**メソッドの説明を参照してください。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

 

 






