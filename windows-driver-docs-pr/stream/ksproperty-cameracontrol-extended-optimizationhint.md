---
title: KSK プロパティ \_ CAMERACONTROL \_ EXTENDED \_ OPTIMIZATIONHINT (アプリケーションパフォーマンス戦略)
description: カメラドライバーは、アプリケーションによって提供されるヒントに基づいて、キャプチャ操作を最適化することができます。 このプロパティは、最も頻繁に使用される操作に基づいて、パフォーマンス戦略を設定するようにドライバーに通知します。
ms.assetid: FEA3D355-B490-4E67-905D-EE5507E91150
keywords:
- ストリーミングメディアデバイスの KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 07/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: c47be5b181c94a60a788fa16c68a34c7cb43d107
ms.sourcegitcommit: 8b6d83bcedea8c872ec8c7df874344421a39dd57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86128892"
---
# <a name="ksproperty_cameracontrol_extended_optimizationhint-application-performance-strategy"></a>KSK プロパティ \_ CAMERACONTROL \_ EXTENDED \_ OPTIMIZATIONHINT (アプリケーションパフォーマンス戦略)

カメラドライバーは、アプリケーションによって提供されるヒントに基づいて、キャプチャ操作を最適化することができます。 このプロパティは、最も頻繁に使用される操作に基づいて、パフォーマンス戦略を設定するようにドライバーに通知します。 たとえば、写真用に最適化されている場合、カメラドライバーはセンサーの露出速度と解像度を最適化するようにセンサーをプログラミングすることがあります。これにより、フォトキャプチャトリガーからイメージキャプチャまでの待ち時間が短縮されます。 同様に、ビデオ用に最適化されている場合、カメラドライバーは、フレームレートが高く、解像度が低くなるようにセンサーをプログラミングすることがあります。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

| 取得 | オン | 移行先 | プロパティ記述子の型 | プロパティ値の型 |
|--|--|--|--|--|
| はい | はい | フィルター | [**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier) | [**KSCAMERA_EXTENDEDPROP_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) |

プロパティ値 (操作データ) には、 [**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造体と[**KSCAMERA \_ extendedprop \_ 値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)構造体が含まれています。

プロパティデータの合計サイズは**sizeof**(KSCAMERA \_ extendedprop \_ ヘッダー) + **sizeof**(KSCAMERA \_ extendedprop \_ 値) です。 [**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**size**メンバーは、この total property データサイズに設定されます。

[**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**機能**メンバーには、次の1つ以上の最適化ヒントのビットごとの or の組み合わせが含まれています。

| 最適化ヒント | 説明 |
|--|--|
| KSCAMERA \_ EXTENDEDPROP の \_ 最適化の \_ 写真 | カメラ操作は写真用に最適化されています |
| KSCAMERA \_ EXTENDEDPROP の最適化に関する \_ \_ ビデオ | カメラの操作はビデオ用に最適化されています |

[**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーには、カメラに現在設定されている最適化 (1 つの値) が含まれています。

既定の最適化の種類は、KSCAMERA \_ extendedprop \_ optimization \_ PHOTO です。 このプロパティがカメラドライバーでサポートされている場合は、両方の最適化の種類がサポートされている必要があります。

このプロパティコントロールは同期であり、キャンセルできません。

## <a name="remarks"></a>解説

### <a name="optimization-modes"></a>最適化モード

**KSCAMERA \_ EXTENDEDPROP の \_ 最適化の \_ 写真**

KSCAMERA \_ extendedprop 最適化ビデオモードを使用するように明示的に通知されるまで、すべてのカメラドライバーはこのモードである必要があり \_ \_ ます。 このモードの目的は、写真操作用のカメラハードウェアを最適化することです。 このモードでは、ビデオ操作を引き続き機能させる必要があります。

**KSCAMERA \_ EXTENDEDPROP の最適化に関する \_ \_ ビデオ**

このモードは、カメラがビデオ操作に使用される可能性があることを示します。 カメラドライバーは、このモードのビデオ操作のハードウェアを最適化する必要があります。 写真操作は機能している必要がありますが、リソース使用の優先度はビデオ操作用です。

### <a name="getting-the-property"></a>プロパティを取得する

KSPROPERTY TYPE GET 要求に応答すると、 \_ \_ ドライバーは[**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)のメンバーを次のように設定します。

| メンバー | 値 |
|--|--|
| Version | 1 |
| PinId | KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF) |
| サイズ | sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE) |
| 結果 | 0 |
| 機能 | サポートされる最適化値 |
| フラグ | 現在の最適化の値の設定 |

最適化モードが設定されていない場合、ドライバーは**フラグ**を KSCAMERA \_ extendedprop \_ optimization \_ PHOTO (既定値) に設定します。

### <a name="setting-the-property"></a>プロパティの設定

プロパティが設定されている場合、KSK プロパティ \_ 型 \_ の set 要求では、 [**KSCAMERA \_ Extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーに設定する最適化モードが含まれます。

## <a name="requirements"></a>必要条件

**バージョン:** Windows 8.1 以降で使用可能

**ヘッダー:** Ksmedia .h (Ksk を含む)

## <a name="see-also"></a>関連項目

[**KSCAMERA \_ EXTENDEDPROP \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA \_ EXTENDEDPROP \_ 値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
