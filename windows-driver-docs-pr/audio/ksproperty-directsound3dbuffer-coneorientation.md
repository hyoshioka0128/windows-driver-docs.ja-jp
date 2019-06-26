---
title: KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEORIENTATION
description: KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEORIENTATION プロパティが 3D サウンド バッファーの円錐状のサウンド投影の方向を指定します。
ms.assetid: c1253114-a2e4-48ff-8219-d932f182478e
keywords:
- KSPROPERTY_DIRECTSOUND3DBUFFER_CONEORIENTATION オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DBUFFER_CONEORIENTATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: deef57ace89cccbed34b23af2788ad698ff79254
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360569"
---
# <a name="kspropertydirectsound3dbufferconeorientation"></a>KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEORIENTATION


KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEORIENTATION プロパティが 3D サウンド バッファーの円錐状のサウンド投影の方向を指定します。

## <span id="ddk_ksproperty_directsound3dbuffer_coneorientation_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DBUFFER_CONEORIENTATION_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">取得</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ds3dvector" data-raw-source="[&lt;strong&gt;DS3DVECTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ds3dvector)"><strong>DS3DVECTOR</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、型のプロジェクション サウンド コーンの方向を示す DS3DVECTOR の構造です。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEORIENTATION プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

DirectSound 3D バッファーのプロジェクションのサウンド コーンの方向についての詳細については、Microsoft Windows SDK のドキュメントでは、次を参照してください。

-   **VConeOrientation** DS3DBUFFER 構造体のメンバー。

-   **IDirectSound3DBuffer::GetConeOrientation**と**IDirectSound3DBuffer::SetConeOrientation**メソッド。

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
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)

[**DS3DVECTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ds3dvector)

 

 






