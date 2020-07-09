---
title: KSK プロパティ \_ CAMERACONTROL \_ 拡張 \_ PHOTOMODE
description: このプロパティは、カメラの写真モード設定を設定または取得します。
ms.assetid: C9596B85-A07B-4DF7-852F-C9EBF43E1E44
keywords:
- ストリーミングメディアデバイスの KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 07/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: cb615a6005a28ee8c031e8748a908ea0d7d063d0
ms.sourcegitcommit: 8b6d83bcedea8c872ec8c7df874344421a39dd57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86128887"
---
# <a name="ksproperty_cameracontrol_extended_photomode"></a>KSK プロパティ \_ CAMERACONTROL \_ 拡張 \_ PHOTOMODE

このプロパティは、カメラの写真モード設定を設定または取得します。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

| 取得 | オン | 移行先 | プロパティ記述子の型 | プロパティ値の型 |
|--|--|--|--|--|
| はい | はい | フィルター | [**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier) | [**KSCAMERA_EXTENDEDPROP_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) |

プロパティ値 (操作データ) には、 [**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造体と[**KSCAMERA \_ extendedprop \_ photomode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)構造体が含まれています。 これらは、シーケンスモードが設定されている場合に、写真モードと履歴フレーム数を指定します。

目的の写真モードは、 [**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーで設定されます。 Photo モードは、次のいずれかに設定されます。

| 写真モード | 説明 |
|--|--|
| KSCAMERA \_ EXTENDEDPROP \_ PHOTOMODE \_ 通常 | 通常の写真操作 |
| KSCAMERA \_ EXTENDEDPROP \_ PHOTOMODE \_ シーケンス | 写真シーケンスのキャプチャ操作 |

プロパティデータの合計サイズは**sizeof**(KSCAMERA \_ extendedprop \_ ヘッダー) + **sizeof**(KSCAMERA \_ extendedprop \_ photomode) です。 [**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**size**メンバーは、この total property データサイズに設定されます。

> [!NOTE]
> Photo モードの設定は非同期制御操作であり、KSCAMERA \_ extendedprop \_ CAPS \_ Asynccontrol は[**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**機能**メンバーで設定する必要があります。

## <a name="remarks"></a>解説

KSPROPERTY TYPE GET 要求に応答すると、 \_ \_ ドライバーは[**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)のメンバーを次のように設定します。

| メンバー | 値 |
|--|--|
| Version | 1 |
| PinId | フォト pin の pin ID |
| サイズ | sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_PHOTOMODE) |
| 結果 | フォトモードデータを取得しようとしたときのエラー値。 それ以外の場合は、0 に設定されます。 |
| 機能 | KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |
| フラグ | 現在の写真モード |

## <a name="requirements"></a>必要条件

**バージョン:** Windows 8.1 以降で使用可能

**ヘッダー:** Ksmedia .h (Ksk を含む)

## <a name="see-also"></a>関連項目

[**KSCAMERA \_ EXTENDEDPROP \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA \_ EXTENDEDPROP \_ PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)
