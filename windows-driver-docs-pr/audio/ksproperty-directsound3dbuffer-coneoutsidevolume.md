---
title: KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEOUTSIDEVOLUME
description: KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEOUTSIDEVOLUME プロパティが 3D サウンド バッファーの円錐外部サウンドのボリュームを指定します。
ms.assetid: faaa4419-6de4-4417-a9a6-922e60130946
keywords:
- KSPROPERTY_DIRECTSOUND3DBUFFER_CONEOUTSIDEVOLUME オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DBUFFER_CONEOUTSIDEVOLUME
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c6b2cd682e857fb3f902bbc7e5b3b03c5e87579
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332776"
---
# <a name="kspropertydirectsound3dbufferconeoutsidevolume"></a>KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEOUTSIDEVOLUME


KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEOUTSIDEVOLUME プロパティが 3D サウンド バッファーの円錐外部サウンドのボリュームを指定します。

## <span id="ddk_ksproperty_directsound3dbuffer_coneoutsidevolume_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DBUFFER_CONEOUTSIDEVOLUME_KS"></span>


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
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p>LONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) は LONG 型の円錐外部ボリューム レベルを指定します。 ボリューム レベルは、1/100ths デシベル単位で表されます。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEOUTSIDEVOLUME プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

DirectSound 3D バッファーの円錐外部サウンドのボリュームの詳細については、Microsoft Windows SDK のドキュメントでは、次を参照してください。

-   **LConeOutsideVolume** DS3DBUFFER 構造体のメンバー。

-   **IDirectSound3DBuffer::GetOutsideVolume**と**IDirectSound3DBuffer::SetOutsideVolume**メソッド。

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


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

 

 






