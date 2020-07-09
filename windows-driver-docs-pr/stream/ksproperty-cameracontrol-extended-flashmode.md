---
title: KSK プロパティ \_ CAMERACONTROL \_ EXTENDED \_ FLASHMODE (normal および sequence)
description: Flash プロパティコントロールは、カメラの通常モードとシーケンス写真モードの両方に対してフラッシュモード操作を設定します。
ms.assetid: A190CB91-0AC4-4ECC-8C55-F0C48CF7B190
keywords:
- ストリーミングメディアデバイスの KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 07/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: d8cbfbf2fe710df78c1e22a401e5c4cf9e7dd666
ms.sourcegitcommit: 8b6d83bcedea8c872ec8c7df874344421a39dd57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86128877"
---
# <a name="ksproperty_cameracontrol_extended_flashmode-normal-and-sequence"></a>KSK プロパティ \_ CAMERACONTROL \_ EXTENDED \_ FLASHMODE (normal および sequence)

Flash プロパティコントロールは、カメラの通常モードとシーケンス写真モードの両方に対してフラッシュモード操作を設定します。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

| 取得 | オン | 移行先 | プロパティ記述子の型 | プロパティ値の型 |
|--|--|--|--|--|
| はい | はい | フィルター | [**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier) | [**KSCAMERA_EXTENDEDPROP_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) |

プロパティ値 (操作データ) には、 [**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造体と[**KSCAMERA \_ extendedprop \_ 値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)構造体が含まれています。

プロパティデータの合計サイズは**sizeof**(KSCAMERA \_ extendedprop \_ ヘッダー) + **sizeof**(KSCAMERA \_ extendedprop \_ 値) です。 [**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**size**メンバーは、この total property データサイズに設定されます。

[**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**機能**メンバーには、ドライバーでサポートされている次の1つ以上のフラッシュモードのビットごとの or の組み合わせが含まれています。

| フラッシュモード | 説明 |
|--|--|
| KSCAMERA \_ EXTENDEDPROP の \_ フラッシュ \_ オフ | フラッシュがオフになっています。 |
| KSCAMERA \_ EXTENDEDPROP \_ FLASH \_ ON | Flash は既定の強度レベルでオンになっています。 |
| \_ADJUSTABLEPOWER の KSCAMERA EXTENDEDPROP \_ FLASH \_ \_ | フラッシュは特定の電源レベルでオンになっています。 |
| KSCAMERA \_ EXTENDEDPROP \_ FLASH \_ AUTO | フラッシュは照明条件に基づいて自動的に作成されます。 |
| KSCAMERA \_ EXTENDEDPROP \_ FLASH \_ AUTO \_ ADJUSTABLEPOWER | フラッシュは、特定の電源レベルの照明条件に基づいて自動的に作成されます。 |

次の機能フラグは、KSCAMERA extendedprop flash OFF を除き、以前の flash 設定と組み合わせることができ \_ \_ \_ ます。

| フラッシュ機能 | 説明 |
|--|--|
| KSCAMERA \_ EXTENDEDPROP \_ FLASH \_ REDEYEREDUCTION | Redeye リダクション機能を有効にします。 このフラグは、他の設定と組み合わせることができます。 |
| KSCAMERA \_ EXTENDEDPROP \_ FLASH \_ SINGLEFLASH | 1つのトリガーに対してのみ flash を設定します。 カメラがフォトシーケンスモードでない場合、この機能は無視されます。 |
| KSCAMERA \_ EXTENDEDPROP \_ FLASH \_ MULTIFLASHSUPPORTED | すべてのシーケンスフレームで flash をトリガーするように設定します。 カメラがフォトシーケンスモードでない場合、この機能は無視されます。 |

[**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーには、カメラに現在設定されている flash モードが含まれています。

カメラの既定のフラッシュモードは KSCAMERA \_ extendedprop \_ flash \_ OFF です。 カメラが flash をサポートしている場合、KSCAMERA \_ extendedprop \_ flash \_ OFF、KSCAMERA \_ extendedprop \_ flash \_ ON、および KSCAMERA \_ extendedprop flash \_ \_ AUTO が必要なモードです。 KSCAMERA \_ extendedprop の \_ flash \_ AUTO \_ ADJUSTABLEPOWER と KSCAMERA \_ extendedprop の \_ flash \_ auto \_ ADJUSTABLEPOWER モードは省略可能です。

カメラでフォトシーケンスモードがサポートされている場合は、KSCAMERA \_ extendedprop \_ flash singleflash をサポートする flash control プロパティが必要です \_ 。

このプロパティコントロールは同期であり、キャンセルできません。

## <a name="remarks"></a>解説

### <a name="getting-the-property"></a>プロパティを取得する

KSPROPERTY TYPE GET 要求に応答すると、 \_ \_ ドライバーは[**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)のメンバーを次のように設定します。

| メンバー | 値 |
|--|--|
| Version | 1 |
| PinId | KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF) |
| サイズ | sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE) |
| 結果 | 0 |
| 機能 | サポートされている Flash モードの値 |
| フラグ | (現在の flash モード値の設定) &#x7c; (flash 機能フラグ) |

Torch モードが KSCAMERA \_ extendedprop \_ flash \_ on \_ ADJUSTABLEPOWER または KSCAMERA extendedprop flash on ADJUSTABLEPOWER の場合 \_ \_ 、u) \_ \_ [** \_ extendedprop \_ 値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)の**KSCAMERA**メンバーには 0-100 の間の輝度レベルの値が含まれます。 明度が0の場合は最小レベル、輝度が100の場合は最大輝度レベルを示します。 調整可能な電源フラグが設定されていない場合は、正規化された輝度設定の値が**u)** に返されます。

フラッシュモードが設定されていない場合、 **Flags**は KSCAMERA \_ extendedprop \_ flash \_ OFF (既定値) に設定されます。

### <a name="setting-the-property"></a>プロパティの設定

プロパティが設定されている場合、KSK プロパティ \_ 型 \_ の set 要求では、 [**KSCAMERA \_ Extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーには、設定する torch モードが含まれます。 [**KSCAMERA \_ extendedprop の \_ 値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)の**U)** メンバーには、**フラグ**が KSCAMERA \_ extendedprop \_ flash \_ ON \_ ADJUSTABLEPOWER または KSCAMERA \_ extendedprop \_ flash \_ AUTO \_ ADJUSTABLEPOWER の場合に設定する輝度レベルが含まれます。

## <a name="requirements"></a>必要条件

**バージョン:** Windows 8.1 以降で使用可能

**ヘッダー:** Ksmedia .h (Ksk を含む)

## <a name="see-also"></a>関連項目

[**KSCAMERA \_ EXTENDEDPROP \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA \_ EXTENDEDPROP \_ 値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
