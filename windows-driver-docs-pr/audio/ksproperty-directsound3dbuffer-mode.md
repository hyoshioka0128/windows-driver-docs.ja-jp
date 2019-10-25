---
title: KSK プロパティ\_DIRECTSOUND3DBUFFER\_モード
description: KSK プロパティ\_DIRECTSOUND3DBUFFER\_MODE プロパティは、3D サウンドバッファーの処理モードを指定します。
ms.assetid: a3b15544-c534-47ea-a02e-5c8f9ccee414
keywords:
- KSPROPERTY_DIRECTSOUND3DBUFFER_MODE オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DBUFFER_MODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b56f7486f180992c2b319d4f57061aaa2d3d5ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830811"
---
# <a name="ksproperty_directsound3dbuffer_mode"></a>KSK プロパティ\_DIRECTSOUND3DBUFFER\_モード


KSK プロパティ\_DIRECTSOUND3DBUFFER\_MODE プロパティは、3D サウンドバッファーの処理モードを指定します。

## <span id="ddk_ksproperty_directsound3dbuffer_mode_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DBUFFER_MODE_KS"></span>


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
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は ULONG 型で、サウンドバッファーの処理モードを指定します。 モードは、ヘッダーファイル Dsound で定義されている次のいずれかの値を持つことができます。

-   DS3DMODE\_通常

-   DS3DMODE\_ヘッド相対

-   DS3DMODE\_DISABLE

これらのパラメーターの意味については、Microsoft Windows SDK のドキュメントを参照してください。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_DIRECTSOUND3DBUFFER\_MODE プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

DirectSound 3D バッファーの処理モードの詳細については、Windows SDK のドキュメントで次の情報を参照してください。

-   DS3DBUFFER 構造体の**Dwmode**メンバー。

-   **IDirectSound3DBuffer:: getmode**メソッドと**IDirectSound3DBuffer:: setmode**メソッド。

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

 

 






