---
title: KSK プロパティ\_CAMERACONTROL\_露出\_相対的
description: KSK プロパティ\_CAMERACONTROL\_露光\_相対プロパティは、電子シャッター速度を指定します。
ms.assetid: a4003fcd-9dc8-4889-9ce0-e4f09273d152
keywords:
- KSPROPERTY_CAMERACONTROL_EXPOSURE_RELATIVE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXPOSURE_RELATIVE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3039b8c504099530266d6877287fd9c99d5ef3bf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843249"
---
# <a name="ksproperty_cameracontrol_exposure_relative"></a>KSK プロパティ\_CAMERACONTROL\_露出\_相対的


KSK プロパティ\_CAMERACONTROL\_露光\_相対プロパティは、電子シャッター速度を指定します。

## <span id="ddk_ksproperty_cameracontrol_exposure_relative_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_EXPOSURE_RELATIVE_KS"></span>


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
<td><p>[はい]</p></td>
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、カメラの相対露出設定を指定する LONG です。 ステップサイズはハードウェアに依存します。 ステップのサイズを確認するには、 [**CAMERACONTROL\_露光プロパティ\_Ksk プロパティ**](ksproperty-cameracontrol-exposure.md)で get 要求を作成します。

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
<td><p>公開時間を実装固有の既定値に設定します。</p></td>
</tr>
<tr class="even">
<td><p>正の値</p></td>
<td><p>露出時間を1ステップずつインクリメントします。</p></td>
</tr>
<tr class="odd">
<td><p>負の値</p></td>
<td><p>露出時間を1ステップずつ減らします。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

Set 要求を行うときには、前の表の値のいずれかを、\_CAMERACONTROL\_NODE\_S 構造体の KSK プロパティの**値**メンバーで指定する必要があります。

Get 要求を行うと、クライアントは、前の表の値のいずれかを、\_CAMERACONTROL\_NODE\_S 構造体の KSK プロパティの値メンバーで受け取ります。 値は、カメラの現在の露出時間の設定を示します。

自動露出モードコントロールが Auto モードまたはアパーチャ優先度モードの場合、セット要求は失敗します。

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

 

 






