---
title: KSPROPERTY\_CAMERACONTROL\_プライバシー
description: KSPROPERTY\_CAMERACONTROL\_プライバシー プロパティでは、カメラ、センサーによって取得されてからビデオを防止するかどうかを指定します。
ms.assetid: 6a96301e-b4f1-4d4d-9cc6-f0cb1e2c1391
keywords:
- KSPROPERTY_CAMERACONTROL_PRIVACY ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_PRIVACY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3969cb1b60910b060e19e6295c2d2b849d3fe679
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536174"
---
# <a name="kspropertycameracontrolprivacy"></a>KSPROPERTY\_CAMERACONTROL\_プライバシー


KSPROPERTY\_CAMERACONTROL\_プライバシー プロパティでは、カメラ、センサーによって取得されてからビデオを防止するかどうかを指定します。

## <span id="ddk_ksproperty_cameracontrol_privacy_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_PRIVACY_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564439" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564439)"><strong>KSPROPERTY_CAMERACONTROL_S</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff564420" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564420)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、プライバシー モードかどうかを指定する LONG を有効にするにはまたは無効になっています。 値が 0 のことを示し、カメラ センサーがビデオのイメージをキャプチャできます 1 の値は、ビデオのイメージのキャプチャからカメラ センサーが禁止されていることを示します。

<a name="remarks"></a>注釈
-------

**値**、KSPROPERTY のメンバー\_CAMERACONTROL\_ノード\_の構造は、カメラ センサーがビデオをキャプチャする必要があるかどうかを指定します。

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
<td><p>Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY\_CAMERACONTROL\_ノード\_S**](https://msdn.microsoft.com/library/windows/hardware/ff564420)

 

 






