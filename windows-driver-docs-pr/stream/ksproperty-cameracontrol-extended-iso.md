---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_ISO
description: このプロパティは、カメラの ISO 設定を選択します。 ISO 設定がプリセットのグループから選択したか、自動に設定します。
ms.assetid: 8BA03479-2AB8-4390-83F0-84C3519DB991
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ISO ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ISO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3a57ec270ab4f89fcaade89367884cba07c1a571
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326000"
---
# <a name="kspropertycameracontrolextendediso"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_ISO


このプロパティは、カメラの ISO 設定を選択します。 ISO 設定がプリセットのグループから選択したか、自動に設定します。

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
<td><p>〇</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と[ **KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)構造体。 **KSCAMERA\_EXTENDEDPROP\_値**必要なが使用されません。

プロパティの合計データ サイズが**sizeof**(KSCAMERA\_EXTENDEDPROP\_ヘッダー) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_値)。 **サイズ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)はこのプロパティの合計データ サイズに設定します。

**機能**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) ISO の次の 1 つ以上のビット演算 OR の組み合わせが含まれています設定。

| ISO                                | 説明                   |
|------------------------------------|-------------------------------|
| KSCAMERA\_EXTENDEDPROP\_ISO\_自動  | ISO 設定は自動です。 |
| KSCAMERA\_EXTENDEDPROP\_ISO\_50    | ISO 50                        |
| KSCAMERA\_EXTENDEDPROP\_ISO\_80    | ISO 80                        |
| KSCAMERA\_EXTENDEDPROP\_ISO\_100   | ISO 100                       |
| KSCAMERA\_EXTENDEDPROP\_ISO\_200   | ISO 200                       |
| KSCAMERA\_EXTENDEDPROP\_ISO\_400   | ISO 400                       |
| KSCAMERA\_EXTENDEDPROP\_ISO\_800   | ISO 800                       |
| KSCAMERA\_EXTENDEDPROP\_ISO\_1600  | ISO 1600                      |
| KSCAMERA\_EXTENDEDPROP\_ISO\_3200  | ISO 3200                      |
| KSCAMERA\_EXTENDEDPROP\_ISO\_6400  | ISO 6400                      |
| KSCAMERA\_EXTENDEDPROP\_ISO\_12800 | ISO 12800                     |
| KSCAMERA\_EXTENDEDPROP\_ISO\_25600 | ISO 25600                     |

 

**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)カメラの現在の ISO 設定が含まれています。 カメラのドライバーでは、ISO 設定のサブセットをサポート可能性があります。 このプロパティのコントロールがサポートされている場合、ドライバーが KSCAMERA をサポートする必要があります\_EXTENDEDPROP\_ISO\_自動。

このプロパティのコントロールは、非同期およびないキャンセル可能なは。

## <a name="remarks"></a>注釈

### <a name="getting-the-property"></a>プロパティを取得

KSPROPERTY に応答するとき\_型\_GET 要求をドライバーのメンバーの設定、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)に、次の場合。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Member</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>バージョン</td>
<td>1</td>
</tr>
<tr class="even">
<td>PinId</td>
<td>写真の暗証番号 (pin) の暗証番号 (pin) の ID。</td>
</tr>
<tr class="odd">
<td>サイズ</td>
<td><p>sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VALUE)</p></td>
</tr>
<tr class="even">
<td>結果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>機能</td>
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |(ISO サポートされている設定)。</td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>現在 ISO 値の設定 (1 つの値)。</td>
</tr>
</tbody>
</table>

 

ISO が既に設定されていない場合、**フラグ**KSCAMERA に設定されている\_EXTENDEDPROP\_ISO\_自動 (既定値)。

### <a name="setting-the-property"></a>プロパティの設定

設定すると、プロパティを KSPROPERTY\_型\_セットの要求、**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) ISO 設定有効にするのににはが含まれます。

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

[KSCAMERA\_EXTENDEDPROP\_ヘッダー](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[KSCAMERA\_EXTENDEDPROP\_値](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)
