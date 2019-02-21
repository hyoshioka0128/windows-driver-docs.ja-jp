---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_CAMERAANGLEOFFSET
description: カメラの角度オフセット プロパティでは、読み取り専用のカメラの位置のピッチ、ヨー角度に関する情報を提供します。 ピッチ、ヨー角度を定義して、水平および垂直の軸からのオフセットします。
ms.assetid: 06F62EB9-DAF7-486F-9940-24EA2224BCB0
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_CAMERAANGLEOFFSET ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_CAMERAANGLEOFFSET
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 95ae39693bc962ecc1ca5fb1c1a99a00cea1fe71
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530339"
---
# <a name="kspropertycameracontrolextendedcameraangleoffset"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_CAMERAANGLEOFFSET

カメラの角度オフセット プロパティでは、読み取り専用のカメラの位置のピッチ、ヨー角度に関する情報を提供します。 ピッチ、ヨー角度を定義して、水平および垂直の軸からのオフセットします。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

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
<td><p>X</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と[ **KSCAMERA\_EXTENDEDPROP\_FIELDOFVIEW** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_fieldofview)構造体。

プロパティの合計データ サイズが**sizeof**(KSCAMERA\_EXTENDEDPROP\_ヘッダー) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_FIELDOFVIEW)。 **サイズ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)はこのプロパティの合計データ サイズに設定します。

**機能**と**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)は使用されませんこのプロパティ。

ドライバーは、カメラの適切な視野を特定できない場合、ドライバーにはこのプロパティのサポートをする必要があります示しません。

このプロパティのコントロールは、同期およびないキャンセル可能なは。

## <a name="remarks"></a>注釈

カメラ センサーおよびジャイロ センサーを同じ物理シャーシ内に保存された場合、は、カメラのドライバーが 0 度があります。 適切なオフセット角度を報告することをお勧めします。 カメラ センサーおよびジャイロ センサーは、同じ物理シャーシに収容されていない、ドライバーはこのプロパティのサポートは指定するお勧めします。

### <a name="getting-the-property"></a>プロパティを取得

KSPROPERTY に応答するとき\_型\_GET 要求をドライバーのメンバーの設定、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)に、次の場合。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メンバー</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>バージョン</td>
<td>1</td>
</tr>
<tr class="even">
<td>PinId</td>
<td>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0 XFFFFFFFF) です。</td>
</tr>
<tr class="odd">
<td>サイズ</td>
<td><p>sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_CAMERAOFFSET)</p></td>
</tr>
<tr class="even">
<td>結果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>機能</td>
<td>0</td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>0</td>
</tr>
</tbody>
</table>

 

ドライバーの角度オフセットの設定、 [ **KSCAMERA\_EXTENDEDPROP\_CAMERAOFFSET** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_cameraoffset)構造体。

## <a name="requirements"></a>要件

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows 8.1 以降を利用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA\_EXTENDEDPROP\_CAMERAOFFSET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_cameraoffset)
