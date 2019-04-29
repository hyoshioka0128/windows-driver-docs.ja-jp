---
title: KSPROPERTY\_DIRECTSOUND3DLISTENER\_バッチ
description: KSPROPERTY\_DIRECTSOUND3DLISTENER\_バッチ プロパティは、3 D リスナーのバッチ モード設定を指定します。
ms.assetid: 370191f8-e5a2-40f0-a979-c14cf7f44756
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_BATCH オーディオ デバイス
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
ms.openlocfilehash: c4e79b3d45e2801584e7048504c860c2246a3d45
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332759"
---
# <a name="kspropertydirectsound3dlistenerbatch"></a>KSPROPERTY\_DIRECTSOUND3DLISTENER\_バッチ


KSPROPERTY\_DIRECTSOUND3DLISTENER\_バッチ プロパティは、3 D リスナーのバッチ モード設定を指定します。

## <span id="ddk_ksproperty_directsound3dlistener_batch_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_BATCH_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) は BOOL 型のバッチ モードの設定を指定します。

-   このプロパティの値が**TRUE**、ミニポート ドライバーには、リスナーのプロパティに対するすべての変更と関連付けられているバッファーのすべてのプロパティをキャッシュする必要があります。

-   値が**FALSE**リスナーのプロパティとバッファーのプロパティの変更は直ちに有効です。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_DIRECTSOUND3DLISTENER\_バッチ プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティが遷移するときに**TRUE**に**FALSE**ミニポート ドライバーは有効にキャッシュされているすべてのプロパティをすぐに配置する必要があります。 可能であれば、任意のキャッシュされたプロパティ導入すべき効果に同時にします。

3D リスナーのバッチ モードの設定の詳細については、の説明を参照して、 **IDirectSound3DListener::CommitDeferredSettings** Microsoft Windows SDK のドキュメント内のメソッド。

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

 

 






