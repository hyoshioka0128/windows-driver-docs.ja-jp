---
title: KSK プロパティ\_CAMERACONTROL\_虹彩\_相対
description: KSK プロパティ\_CAMERACONTROL\_虹彩\_相対プロパティは、カメラの絞りの設定を指定します。
ms.assetid: 919fcf7a-ee96-4e1e-b0ce-e5a7ce5086c7
keywords:
- KSPROPERTY_CAMERACONTROL_IRIS_RELATIVE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_IRIS_RELATIVE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4952ae28463244efa358d843fd2ddf1d660b59cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843351"
---
# <a name="ksproperty_cameracontrol_iris_relative"></a>KSK プロパティ\_CAMERACONTROL\_虹彩\_相対


KSK プロパティ\_CAMERACONTROL\_虹彩\_相対プロパティは、カメラの絞りの設定を指定します。

## <span id="ddk_ksproperty_cameracontrol_iris_relative_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_IRIS_RELATIVE_KS"></span>


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
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、カメラの相対虹彩設定を指定する LONG です。 虹彩の手順のサイズとアイリスの手順の既定値の両方が実装固有であることに注意してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>虹彩を既定のオープンに設定します。 この既定値は実装固有であり、ハードウェアで提供されます。</p></td>
</tr>
<tr class="even">
<td><p>正の値</p></td>
<td><p>虹彩の1ステップを開きます。</p></td>
</tr>
<tr class="odd">
<td><p>負の値</p></td>
<td><p>虹彩の1ステップを閉じます。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

Set 要求を行うときには、前の表の値のいずれかを、\_CAMERACONTROL\_NODE\_S 構造体の KSK プロパティの**値**メンバーで指定する必要があります。

自動露出モードコントロールが自動モードまたはシャッター優先度モードの場合、設定要求は失敗します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY\_CAMERACONTROL\_NODE\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)

 

 






