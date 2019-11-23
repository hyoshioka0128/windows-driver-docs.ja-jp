---
title: KSK プロパティ\_CAMERACONTROL\_フォーカス
description: ユーザーモードクライアントは、KSK プロパティ\_CAMERACONTROL\_FOCUS プロパティを使用して、カメラのフォーカス設定を取得または設定します。 このプロパティは省略可能です。
ms.assetid: 89a77055-1ad1-4394-8435-d057685b9eee
keywords:
- ストリーミングメディアデバイスの KSPROPERTY_CAMERACONTROL_FOCUS
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_FOCUS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57ddab6e219133ae4b8ad9e81c6f8003d0939783
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840463"
---
# <a name="ksproperty_cameracontrol_focus"></a>KSK プロパティ\_CAMERACONTROL\_フォーカス


ユーザーモードクライアントは、KSK プロパティ\_CAMERACONTROL\_FOCUS プロパティを使用して、カメラのフォーカス設定を取得または設定します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_cameracontrol_focus_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_FOCUS_KS"></span>


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
<td><p>〇</p></td>
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、フォーカス設定を指定する LONG です。 この値はミリメートル単位で表されます。

**注意**  アプリの作成時またはテスト時には、実際には、一部のドライバーでは、一般的な単位に基づいていない、フォーカス値のカスタム範囲とカスタムステップ値が定義されていることに注意してください。 ドライバーは、物理的またはデジタルのどちらかでフォーカスコントロールを実装する場合があります。

 

<a name="remarks"></a>注釈
-------

CAMERACONTROL\_S 構造体\_KSK プロパティの**値**メンバーは、フォーカス設定を指定します。

このプロパティをサポートするすべてのビデオキャプチャミニドライバーは、このプロパティの独自の範囲と既定値を定義する必要があります。

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
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSK プロパティ\_CAMERACONTROL\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)

 

 






