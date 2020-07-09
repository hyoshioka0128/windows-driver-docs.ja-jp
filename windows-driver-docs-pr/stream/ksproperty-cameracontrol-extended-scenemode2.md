---
title: KSK プロパティ \_ CAMERACONTROL \_ EXTENDED \_ SCENEMODE (ISP コントロールパラメーター)
description: '\_ \_ \_ Ksk プロパティ CAMERACONTROL extended property 列挙で定義されている ksk プロパティ CAMERACONTROL EXTENDED SCENEMODE プロパティ ID を \_ 使用すると、oem は、必要に応じ \_ \_ て、シーンモードとその他の ISP コントロールパラメーターを微調整することができます。'
ms.assetid: CB3F89AD-4B53-4E47-B60E-4B584DB8418B
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
ms.openlocfilehash: 027cf5b3266ce3102692d18417b0eff9d5b8ddd4
ms.sourcegitcommit: 8b6d83bcedea8c872ec8c7df874344421a39dd57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86128867"
---
# <a name="ksproperty_cameracontrol_extended_scenemode-isp-control-parameters"></a>KSK プロパティ \_ CAMERACONTROL \_ EXTENDED \_ SCENEMODE (ISP コントロールパラメーター)

[**Ksk プロパティ \_ CAMERACONTROL \_ extended \_ property**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)列挙で定義されている**KSK プロパティ \_ CAMERACONTROL \_ extended \_ SCENEMODE**プロパティ ID を使用すると、oem は、必要に応じて、シーンモードとその他の ISP コントロールパラメーターを微調整することができます。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

| スコープ | Control | Type |
|--|--|--|
| Version 1 | フィルター | 非同期 |

シーンモードは、特定の条件に対する操作を最適化するためにカメラシステムをガイドするヒントとして使用されます。 シーンモードおよびその他の ISP コントロール (白のバランス、ISO、露出時間、EV 補正など) は、互いに影響を与えることなく、独立して動作できる必要があります。

- 他の ISP コントロールパラメーターを変更しても、既存のシーンモードを変更することはできません。 他の ISP パラメーターを変更した後に、ドライバーはシーンモードを手動に変更する必要はありません。

- 自動シーンモードを設定しても、他の ISP コントロールの既存の設定を変更することはできません。 ドライバーは、他の ISP コントロールのフル自動モードに戻す必要はありません。

**KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ AUTO**

このフラグは、自動シーンモードを示します。 カメラドライバーは、シーンに基づいて最適なシーンモード設定を自動的に決定し、シーンに必要なさまざまな ISP 設定を最適化します。

**KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ MANUAL**

このフラグは適用できません。

**KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ マクロ \\ 縦書き \\ \\ \\ \\ \\ \\ CANDLELIGHT \\ 横 \\ NIGHTPORTRAIT \\ ライトバック**

これらのフラグは、定義されているように、対応するシーンモードを示します。 カメラドライバーでは、必要に応じてさまざまな ISP 設定を最適化するためのヒントとして指定されているシーンモードが使用されます (たとえば、夜の場合、ISP の設定は夜の時間環境向けに最適化されています)。

次の表には、 **Ksk プロパティ \_ CAMERACONTROL \_ EXTENDED \_ SCENEMODE**プロパティを使用する場合の[**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造のフィールドの説明と要件が含まれています。 [**KSCAMERA \_ extendedprop \_ 値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)構造体は、 **ksk プロパティ \_ CAMERACONTROL \_ EXTENDED \_ SCENEMODE**では無視されます。

| メンバー | 値 |
|--|--|
| Version | 1 |
| PinId | KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF) |
| サイズ | sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE) |
| 結果 | これは、最後の設定操作のエラー結果を示します。 設定操作が行われていない場合は、0にする必要があります。 値0は、エラーが検出されなかったことを示します。 |
| 機能 | これは、 **KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL**のビットごとの or であり、上で定義されているサポートされているシーンモードである必要があります。 カメラドライバーがこのコントロールをサポートしている場合は**KSCAMERA_EXTENDEDPROP_SCENEMODE_AUTO**がサポートされている必要があります。 |
| フラグ | これは、上記のサポートされているシーンモードのいずれかになります。 |

## <a name="requirements"></a>必要条件

**ヘッダー:** Ksmedia .h (Ksk を含む)
