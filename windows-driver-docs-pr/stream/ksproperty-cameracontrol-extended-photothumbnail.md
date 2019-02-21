---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOTHUMBNAIL
description: このプロパティを取得またはカメラのサムネイルの機能を設定します。
ms.assetid: 859620FD-02ED-4AA1-83B7-B92517F23B0C
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTHUMBNAIL ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTHUMBNAIL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: a5d721e62301a1e8f6f62b4feb31b46afb10fb55
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535776"
---
# <a name="kspropertycameracontrolextendedphotothumbnail"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOTHUMBNAIL

このプロパティを取得またはカメラのサムネイルの機能を設定します。 スケール ファクターが指定されている場合、選択した大規模サムネイルが有効です。

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

プロパティの値 (データの操作) が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と[ **KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)構造体。 **KSCAMERA\_EXTENDEDPROP\_値**が必要ですが、**値**メンバーは無視されます。

プロパティの合計データ サイズが**sizeof**(KSCAMERA\_EXTENDEDPROP\_ヘッダー) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_値)。 **サイズ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)はこのプロパティの合計データ サイズに設定します。

**機能**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)次の 1 つ以上のビット演算 OR の組み合わせが含まれていますサポートされている値をスケーリングします。

| サムネイルのスケール フラグ                            | 説明                            |
|-------------------------------------------------|----------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_PHOTOTHUMBNAIL\_を無効にします。 | サムネイルは無効です。               |
| KSCAMERA\_EXTENDEDPROP\_PHOTOTHUMBNAIL\_2 X      | サムネイルの解像度が X/2 Y/2 とします。   |
| KSCAMERA\_EXTENDEDPROP\_PHOTOTHUMBNAIL\_2 X      | サムネイルの解像度が X/4 Y/4 とします。   |
| KSCAMERA\_EXTENDEDPROP\_PHOTOTHUMBNAIL\_8 X      | サムネイルの解像度が X/8 Y/8 とします。   |
| KSCAMERA\_EXTENDEDPROP\_PHOTOTHUMBNAIL\_16 X     | サムネイルの解像度が X/16 と Y/16 します。 |

**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)カメラ現在設定されているサムネイル スケール値が含まれています。 サムネイルの生成が有効にする、KSCAMERA 場合\_EXTENDEDPROP\_PHOTOTHUMBNAIL\_無効化が設定されている**フラグ**します。

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
<td>写真の暗証番号 (pin) の暗証番号 (pin) の ID。</td>
</tr>
<tr class="odd">
<td>サイズ</td>
<td><p>sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VALUE)</p></td>
</tr>
<tr class="even">
<td>結果</td>
<td><p>結果から縮小表示の設定を取得しようとすると、エラー値。</p></td>
</tr>
<tr class="odd">
<td>機能</td>
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |(サムネイル スケール サポートされている値)。</td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>現在のサムネイルの値設定 (1 つの値)。</td>
</tr>
</tbody>
</table>

### <a name="setting-the-property"></a>プロパティの設定

設定すると、プロパティを KSPROPERTY\_型\_セットの要求、**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)サムネイル スケール フラグのいずれかが含まれます。

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

[**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
