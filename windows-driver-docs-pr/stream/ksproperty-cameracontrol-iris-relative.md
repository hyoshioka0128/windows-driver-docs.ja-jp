---
title: KSPROPERTY\_CAMERACONTROL\_IRIS\_相対
description: KSPROPERTY\_CAMERACONTROL\_IRIS\_相対プロパティは、カメラの絞り設定を指定します。
ms.assetid: 919fcf7a-ee96-4e1e-b0ce-e5a7ce5086c7
keywords:
- KSPROPERTY_CAMERACONTROL_IRIS_RELATIVE ストリーミング メディア デバイス
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
ms.openlocfilehash: c9c4282e334b04a6cccebd3011524fd335ccc1c6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384492"
---
# <a name="kspropertycameracontrolirisrelative"></a>KSPROPERTY\_CAMERACONTROL\_IRIS\_相対


KSPROPERTY\_CAMERACONTROL\_IRIS\_相対プロパティは、カメラの絞り設定を指定します。

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
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong> </a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、カメラの相対あやめの設定を指定する LONG が。 あやめのステップのサイズと iris ステップの既定値は実装に固有であることに注意してください。

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
<td><p>既定の開始、iris を設定します。 この既定値は実装に固有とハードウェアで指定します。</p></td>
</tr>
<tr class="even">
<td><p>正の値</p></td>
<td><p>あやめの 1 つの手順を開きます。</p></td>
</tr>
<tr class="odd">
<td><p>負の値</p></td>
<td><p>あやめの 1 つの手順を閉じます。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

セットの要求を行うときで上記のテーブル内の値のいずれかを指定する必要があります、**値**、KSPROPERTY のメンバー\_CAMERACONTROL\_ノード\_S 構造体。

自動露出モードの制御が自動モードまたはシャッター優先モードの場合、一連の要求は失敗します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY\_CAMERACONTROL\_ノード\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)

 

 






