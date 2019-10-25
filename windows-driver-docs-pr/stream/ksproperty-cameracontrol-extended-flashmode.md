---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FLASHMODE
description: Flash プロパティコントロールは、カメラの通常モードとシーケンス写真モードの両方に対してフラッシュモード操作を設定します。
ms.assetid: A190CB91-0AC4-4ECC-8C55-F0C48CF7B190
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE ストリーミングメディアデバイス
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
ms.openlocfilehash: 11dd98552f76e8e88d585cb8a7e536a0965ceea6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843231"
---
# <a name="ksproperty_cameracontrol_extended_flashmode"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FLASHMODE


Flash プロパティコントロールは、カメラの通常モードとシーケンス写真モードの両方に対してフラッシュモード操作を設定します。

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
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) には、 [**KSCAMERA\_extendedprop\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と、 [**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)の構造体が含まれています。

プロパティデータの合計サイズは**sizeof**(KSCAMERA\_extendedprop\_HEADER) + **sizeof**(KSCAMERA\_extendedprop\_値) です。 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**size**メンバーは、この total property データサイズに設定されます。

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**機能**メンバーには、ドライバーでサポートされている次の1つ以上のフラッシュモードのビットごとの or の組み合わせが含まれています。

| フラッシュモード                                           | 説明                                                                |
|------------------------------------------------------|----------------------------------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_FLASH\_OFF                   | フラッシュがオフになっています。                                                              |
| KSCAMERA\_EXTENDEDPROP\_FLASH\_                    | Flash は既定の強度レベルでオンになっています。                                |
| KSCAMERA\_EXTENDEDPROP\_\_ADJUSTABLEPOWER での FLASH\_   | フラッシュは特定の電源レベルでオンになっています。                                     |
| KSCAMERA\_EXTENDEDPROP\_FLASH\_AUTO                  | フラッシュは照明条件に基づいて自動的に作成されます。                           |
| KSCAMERA\_EXTENDEDPROP\_FLASH\_AUTO\_ADJUSTABLEPOWER | フラッシュは、特定の電源レベルの照明条件に基づいて自動的に作成されます。 |

 

次の機能フラグは、KSCAMERA\_EXTENDEDPROP\_FLASH\_OFF を除き、以前の flash 設定と組み合わせることができます。

| フラッシュ機能 | 説明 |
|---|---|
| KSCAMERA\_EXTENDEDPROP\_FLASH\_REDEYEREDUCTION | Redeye リダクション機能を有効にします。 このフラグは、他の設定と組み合わせることができます。 |
| KSCAMERA\_EXTENDEDPROP\_FLASH\_SINGLEFLASH | 1つのトリガーに対してのみ flash を設定します。 カメラがフォトシーケンスモードでない場合、この機能は無視されます。 |
| KSCAMERA\_EXTENDEDPROP\_FLASH\_MULTIFLASHSUPPORTED | すべてのシーケンスフレームで flash をトリガーするように設定します。 カメラがフォトシーケンスモードでない場合、この機能は無視されます。 |

 

[**KSCAMERA\_EXTENDEDPROP\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーには、カメラに現在設定されている flash モードが含まれています。

カメラの既定のフラッシュモードは、KSCAMERA\_EXTENDEDPROP\_FLASH\_OFF です。 カメラが flash をサポートしている場合、KSCAMERA\_EXTENDEDPROP\_FLASH\_OFF、KSCAMERA\_EXTENDEDPROP\_FLASH\_ON、および KSCAMERA\_EXTENDEDPROP\_FLASH\_AUTO が必要なモードになります。 KSCAMERA\_EXTENDEDPROP\_FLASH\_AUTO\_ADJUSTABLEPOWER および KSCAMERA\_EXTENDEDPROP\_FLASH\_AUTO\_ADJUSTABLEPOWER モードは省略可能です。

カメラでフォトシーケンスモードがサポートされている場合、flash control プロパティは、KSCAMERA\_EXTENDEDPROP\_FLASH\_SINGLEFLASH をサポートするために必要です。

このプロパティコントロールは同期であり、キャンセルできません。

## <a name="remarks"></a>注釈

### <a name="getting-the-property"></a>プロパティを取得する

\_GET 要求の種類\_KSK プロパティに応答すると、ドライバーは、 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)のメンバーを次のように設定します。

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
<td>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF)。</td>
</tr>
<tr class="odd">
<td>Size</td>
<td><p>sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE)</p></td>
</tr>
<tr class="even">
<td>結果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>機能</td>
<td>Flash モードの値がサポートされています。</td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>(現在の flash モード値の設定) |(フラッシュ機能フラグ)</td>
</tr>
</tbody>
</table>

 

Torch モードが KSCAMERA\_EXTENDEDPROP\_FLASH\_ON\_ADJUSTABLEPOWER または KSCAMERA\_EXTENDEDPROP\_\_ADJUSTABLEPOWER で**の u) のメンバー** [**KSCAMERA\_11_ EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)は、0-100 の間の輝度レベルの値を含みます。 明度が0の場合は最小レベル、輝度が100の場合は最大輝度レベルを示します。 調整可能な電源フラグが設定されていない場合は、正規化された輝度設定の値が**u)** に返されます。

フラッシュモードが設定されていない場合、 **Flags**は KSCAMERA\_extendedprop\_FLASH\_OFF (既定) に設定されます。

### <a name="setting-the-property"></a>プロパティの設定

プロパティが設定されている場合、KSK プロパティ\_TYPE\_SET 要求では、 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーに設定する torch モードが含まれます。 [**KSCAMERA\_extendedprop\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)の**u)** メンバーには、**フラグ**が KSCAMERA\_EXTENDEDPROP\_FLASH\_ON\_ADJUSTABLEPOWER または KSCAMERA である場合に設定する輝度レベルが含まれ\_EXTENDEDPROP\_FLASH\_AUTO\_ADJUSTABLEPOWER。

## <a name="requirements"></a>要件

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows 8.1 以降で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
