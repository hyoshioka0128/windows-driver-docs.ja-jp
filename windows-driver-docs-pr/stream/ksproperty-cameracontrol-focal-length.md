---
title: KSPROPERTY \_ CAMERACONTROL の \_ 焦点の \_ 長さ
description: KSK プロパティ CAMERACONTROL の " \_ \_ 焦点 \_ 長" プロパティは、カメラの焦点の長さの情報を取得します。
ms.assetid: a7fba5e4-abd1-46ae-b93c-5fede0249771
keywords:
- ストリーミングメディアデバイスの KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: d5417e7a996a10a50880bd364aecd0119b166268
ms.sourcegitcommit: 8143bb312ead6582b4b3e0ad34b6266dcfd74fb5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84992470"
---
# <a name="ksproperty_cameracontrol_focal_length"></a>KSPROPERTY \_ CAMERACONTROL の \_ 焦点の \_ 長さ

KSK プロパティ CAMERACONTROL の " \_ \_ 焦点 \_ 長" プロパティは、カメラの焦点の長さの情報を取得します。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

| 取得 | オン | 移行先 | プロパティ記述子の型 | プロパティ値の型 |
|--|--|--|--|--|
| はい | いいえ | フィルターまたはノード | [**KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_focal_length_s)または[ **KSPROPERTY_CAMERACONTROL_NODE_FOCAL_LENGTH_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_focal_length_s) | LONG |

プロパティ値 (操作データ) は、カメラの焦点距離を指定する LONG です。

## <a name="remarks"></a>Remarks

このプロパティ要求を使用して、ズーム値を解釈できます。 ズームの範囲は、 **lObjectiveFocalLengthMin** / **lOcularFocalLength**と**lObjectiveFocalLengthMax** / **lOcularFocalLength**の間にする必要があります。 (**lOcularFocalLength**、 **LObjectiveFocalLengthMin**、および**lObjectiveFocalLengthMax**は、 [**ksproperty CAMERACONTROL の \_ \_ 焦点の \_ 長さ \_ s**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_focal_length_s)と[**ksk プロパティ \_ CAMERACONTROL \_ NODE \_ の \_ 焦点 \_ **](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_focal_length_s)となる長さの構造体のメンバーです)。

たとえば、 **lObjectiveFocalLengthMax** = 105 および**lOcularFocalLength** = 35 の場合、このカメラは、最大光学ズーム比105/35 または3に対応しています。

USB Video Class Device Class specification の「*光学ズーム*」セクションも参照してください。 この仕様は、 [USB 実装者フォーラム](https://www.usb.org/)の web サイトで入手できます。

## <a name="requirements"></a>必要条件

| &nbsp; | &nbsp; |
| --- | --- |
| **ヘッダー** | Ksmedia .h (Ksk を含む) |

## <a name="see-also"></a>関連項目

[**KSPROPERTY \_ CAMERACONTROL の \_ 焦点の \_ 長さ \_ S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_focal_length_s)

[**KSPROPERTY \_ CAMERACONTROL \_ NODE の \_ 焦点の \_ 長さ \_ S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_focal_length_s)

[**KSK プロパティ \_ CAMERACONTROL \_ ZOOM**](ksproperty-cameracontrol-zoom.md)

[**KSK プロパティ \_ CAMERACONTROL \_ ZOOM \_ 相対値**](ksproperty-cameracontrol-zoom-relative.md)
