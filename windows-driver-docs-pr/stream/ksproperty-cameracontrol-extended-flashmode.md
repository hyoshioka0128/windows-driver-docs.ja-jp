---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_FLASHMODE
description: フラッシュ プロパティ コントロールは、フラッシュのモードで両方の通常の操作とカメラのシーケンスの写真のモードを設定します。
ms.assetid: A190CB91-0AC4-4ECC-8C55-F0C48CF7B190
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8c404292ba7d4282de28bad588cd35b42a87b76c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530264"
---
# <a name="kspropertycameracontrolextendedflashmode"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_FLASHMODE


フラッシュ プロパティ コントロールは、フラッシュのモードで両方の通常の操作とカメラのシーケンスの写真のモードを設定します。

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
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と[ **KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)構造体。

プロパティの合計データ サイズが**sizeof**(KSCAMERA\_EXTENDEDPROP\_ヘッダー) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_値)。 **サイズ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)はこのプロパティの合計データ サイズに設定します。

**機能**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)次の 1 つ以上のビット演算 OR の組み合わせが含まれていますドライバーによってサポートされているモードをフラッシュします。

| フラッシュ モード                                           | 説明                                                                |
|------------------------------------------------------|----------------------------------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_FLASH\_OFF                   | Flash がオフです。                                                              |
| KSCAMERA\_EXTENDEDPROP\_FLASH\_ON                    | Flash は、既定の強度レベルでは。                                |
| KSCAMERA\_EXTENDEDPROP\_FLASH\_ON\_ADJUSTABLEPOWER   | Flash は、特定の電源レベルでは。                                     |
| KSCAMERA\_EXTENDEDPROP\_FLASH\_自動                  | Flash は、照明の条件に基づく自動です。                           |
| KSCAMERA\_EXTENDEDPROP\_FLASH\_自動\_ADJUSTABLEPOWER | Flash は、特定の電源レベルで照明条件に基づく自動です。 |

 

次の機能フラグを除く KSCAMERA フラッシュ以前の設定と組み合わせることができます\_EXTENDEDPROP\_FLASH\_OFF。

| フラッシュの機能 | 説明 |
|---|---|
| KSCAMERA\_EXTENDEDPROP\_FLASH\_REDEYEREDUCTION | 赤の軽減機能を有効にします。 このフラグは、それ以外の設定と組み合わせることができます。 |
| KSCAMERA\_EXTENDEDPROP\_FLASH\_SINGLEFLASH | トリガーの 1 つだけのフラッシュを設定します。 この機能には、カメラで写真シーケンス モードでない場合は無視されます。 |
| KSCAMERA\_EXTENDEDPROP\_FLASH\_MULTIFLASHSUPPORTED | シーケンス フレームごとにフラッシュするトリガーを設定します。 この機能には、カメラで写真シーケンス モードでない場合は無視されます。 |

 

**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)現在設定されて、カメラのフラッシュ モードが含まれています。

カメラのフラッシュの既定のモードは KSCAMERA\_EXTENDEDPROP\_FLASH\_OFF。 カメラは、flash、KSCAMERA をサポートしている場合\_EXTENDEDPROP\_FLASH\_KSCAMERA オフ\_EXTENDEDPROP\_FLASH\_ON、および KSCAMERA\_EXTENDEDPROP\_FLASH\_自動が必要なモードです。 KSCAMERA\_EXTENDEDPROP\_FLASH\_自動\_ADJUSTABLEPOWER と KSCAMERA\_EXTENDEDPROP\_FLASH\_自動\_ADJUSTABLEPOWER モードは、省略可能。

フラッシュのコントロールのプロパティが KSCAMERA 対応の必要な場合は、カメラで写真シーケンス モードがサポートされている、\_EXTENDEDPROP\_FLASH\_SINGLEFLASH します。

このプロパティのコントロールは、同期およびないキャンセル可能なは。

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
<td>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0 XFFFFFFFF) です。</td>
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
<td>フラッシュ モード値がサポートされています。</td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>(現在フラッシュ モード値の設定) |(flash の機能フラグ)</td>
</tr>
</tbody>
</table>

 

Torch モードが KSCAMERA が場合\_EXTENDEDPROP\_FLASH\_ON\_ADJUSTABLEPOWER または KSCAMERA\_EXTENDEDPROP\_FLASH\_ON\_ADJUSTABLEPOWER、、 **Value.ull**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value) 0 - 間の輝度レベル値を含む 100。 0 の輝度は最小レベルを示し、100 の輝度が最大輝度レベルを示します。 調整可能な power フラグが設定されていない場合で正規化された強度設定の値が返されます。 **Value.ull**します。

フラッシュ モードが既に設定されていない場合、し**フラグ**KSCAMERA に設定されている\_EXTENDEDPROP\_FLASH\_OFF (既定)。

### <a name="setting-the-property"></a>プロパティの設定

設定すると、プロパティを KSPROPERTY\_型\_セットの要求、**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)設定 torch モードにが含まれます。 **Value.ull**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)場合に設定する強度レベルを含む**フラグ**は KSCAMERA\_EXTENDEDPROP\_FLASH\_ON\_ADJUSTABLEPOWER または KSCAMERA\_EXTENDEDPROP\_FLASH\_自動\_ADJUSTABLEPOWER します。

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
