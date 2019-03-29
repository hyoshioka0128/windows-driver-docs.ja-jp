---
title: KSPROPERTY\_CAMERACONTROL\_ロール
description: ユーザー モードのクライアントの使用、KSPROPERTY\_CAMERACONTROL\_ロール プロパティを取得またはカメラのロールの設定を設定します。 このプロパティは省略可能です。
ms.assetid: 58b09e8d-7c0c-4e32-b124-5722bd09f011
keywords:
- KSPROPERTY_CAMERACONTROL_ROLL ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_ROLL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8d6c72f6f140f60fa492e25bde89bca5fa5fc1b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571535"
---
# <a name="kspropertycameracontrolroll"></a>KSPROPERTY\_CAMERACONTROL\_ロール


ユーザー モードのクライアントの使用、KSPROPERTY\_CAMERACONTROL\_ロール プロパティを取得またはカメラのロールの設定を設定します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_cameracontrol_roll_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_ROLL_KS"></span>


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
<th>Set</th>
<th>移行先</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564439" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564439)"><strong>KSPROPERTY_CAMERACONTROL_S</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff564420" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564420)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、カメラのロールの設定を指定する LONG が。 この値は度数で表されます。

正の値では、画像表示の軸に沿ったカメラの時計回りの回転が発生します。 負の値では、次の図に示すように、カメラの反時計回りに回転が発生します。

![図が表示されたカメラ ロール値](images/cam-roll-1.png)

このプロパティをサポートするすべてのビデオ キャプチャ ミニドライバーには、このプロパティの値を範囲と既定値を定義する必要があります。 デバイスの範囲は-180 +180 経由である必要があり、既定値は 0 である必要があります。

<a name="remarks"></a>コメント
-------

**値**、KSPROPERTY のメンバー\_CAMERACONTROL\_の構造は、ロール設定を指定します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_CAMERACONTROL\_S**](https://msdn.microsoft.com/library/windows/hardware/ff564439)

 

 






