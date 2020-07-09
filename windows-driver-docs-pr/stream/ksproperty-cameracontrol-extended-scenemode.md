---
title: KSK プロパティ \_ CAMERACONTROL \_ EXTENDED \_ SCENEMODE (ドライバー定義モード)
description: シーンモードプロパティは、事前設定されたコントロールのコレクションを表すドライバー定義モードを選択します。
ms.assetid: 32C350FF-AA54-4F28-8AD2-341A31648B60
keywords:
- ストリーミングメディアデバイスの KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 07/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 0a1d59383651569b4d194b5dd424fa587140e2bf
ms.sourcegitcommit: 8b6d83bcedea8c872ec8c7df874344421a39dd57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86128865"
---
# <a name="ksproperty_cameracontrol_extended_scenemode-driver-defined-mode"></a>KSK プロパティ \_ CAMERACONTROL \_ EXTENDED \_ SCENEMODE (ドライバー定義モード)

シーンモードプロパティは、事前設定されたコントロールのコレクションを表すドライバー定義モードを選択します。 ドライバーは、シーンモードに割り当てられているプリセットを特定し、シーンを選択したときにコントロールの設定を有効にします。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

| 取得 | オン | 移行先 | プロパティ記述子の型 | プロパティ値の型 |
|--|--|--|--|--|
| はい | はい | フィルター | [**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier) | [**KSCAMERA_EXTENDEDPROP_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) |

プロパティ値 (操作データ) には、 [**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造体と[**KSCAMERA \_ extendedprop \_ 値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)構造体が含まれています。 **KSCAMERA \_ extendedprop \_ 値**が必要ですが、**値**メンバーは無視されます。

プロパティデータの合計サイズは**sizeof**(KSCAMERA \_ extendedprop \_ ヘッダー) + **sizeof**(KSCAMERA \_ extendedprop \_ 値) です。 [**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**size**メンバーは、この total property データサイズに設定されます。

[**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**機能**メンバーには、ドライバーでサポートされている次のシーンモードの1つ以上のビットごとの or の組み合わせが含まれています。

| シーンモード | 説明 |
|--|--|
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ AUTO | 自動匂いモード。 コントロールは、自動的に設定されます。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ マクロ | マクロシーンモード (定義されているドライバー)。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ 縦長 | 縦長シーンモード (定義済みドライバー)。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ スポーツ | スポーツシーンモード (定義されているドライバー)。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ 雪 | 雪シーンモード (定義されているドライバー)。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ 夜 | 夜間シーンモード (定義されているドライバー)。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ ビーチ | ビーチシーンモード (定義されているドライバー)。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ 日没 | 日没シーンモード (定義されているドライバー)。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ CANDLELIGHT | Candlelight シーンモード (定義されているドライバー)。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ ランドスケープ | 横長シーンモード (定義されているドライバー)。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ NIGHTPORTRAIT | 夜間のシーンモード (定義されているドライバー)。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ バックライト | バックライトシーンモード (定義されているドライバー)。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ MANUAL | コントロールが手動で変更され、定義済みのシーンモードは設定されていません。 |

[**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーには、カメラに現在設定されているシーンモードが含まれています。 カメラの既定のシーンモードは、常に KSCAMERA \_ extendedprop \_ SCENEMODE \_ AUTO です。

このプロパティコントロールは非同期であり、キャンセルできません。

## <a name="remarks"></a>解説

### <a name="getting-the-property"></a>プロパティを取得する

KSPROPERTY TYPE GET 要求に応答すると、 \_ \_ ドライバーは[**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)のメンバーを次のように設定します。

| メンバー | 値 |
|--|--|
| Version | 1 |
| PinId | KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF) |
| サイズ | sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE) |
| 結果 | 0 |
| 機能 | KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL &#x7c; (シーンモードの値がサポートされています) |
| フラグ | 現在のシーンモード値の設定 (1 つの値のみ) |

シーンモードが以前に設定されていない場合、 **Flags**は KSCAMERA \_ extendedprop \_ SCENEMODE \_ AUTO (既定値) に設定されます。

### <a name="setting-the-property"></a>プロパティの設定

プロパティが設定されている場合、KSK プロパティ \_ 型 \_ の set 要求では、 [**KSCAMERA \_ Extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーには、有効にするシーンモードが含まれます。

## <a name="requirements"></a>必要条件

**バージョン:** Windows 8.1 以降で使用可能

**ヘッダー:** Ksmedia .h (Ksk を含む)

## <a name="see-also"></a>関連項目

[**KSCAMERA \_ EXTENDEDPROP \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA \_ EXTENDEDPROP \_ 値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
