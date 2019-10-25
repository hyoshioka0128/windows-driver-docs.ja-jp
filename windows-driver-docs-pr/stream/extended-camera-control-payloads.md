---
title: 拡張カメラ コントロール ペイロード
description: KSPROPERTYSETID_ExtendedCameraControl プロパティセット内のコントロールプロパティは、プロパティデータの取得と設定に共通のペイロード形式を使用します。
ms.assetid: 347413DB-229B-40D7-BD3E-931493EE1FBC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b66fe8aa03d98317e20b6a24de91c8fa3760feb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834415"
---
# <a name="extended-camera-control-payloads"></a>拡張カメラ コントロール ペイロード


[Ksk Propertysetid\_ExtendedCameraControl](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropertysetid-extendedcameracontrol)プロパティセット内のコントロールプロパティは、プロパティデータの取得と設定に共通のペイロード形式を使用します。

## <a name="extended-camera-property-header"></a>拡張カメラプロパティヘッダー


すべてのペイロードは、 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造で始まります。 この構造体には、関連付けられたコントロールフラグと機能を持つピンターゲットが含まれます。 特定のコントロールに応じて、**機能**メンバーには、コントロールによって提供される一連の機能が含まれます。 **Flags**メンバーには、現在設定されている、またはコントロールに設定される実際の機能が含まれます。

**Pinid**メンバーは、カメラピンまたはフィルターピンのどちらかであるターゲットを指定します。 プロパティがフィルターレベルのコントロールである場合、 **Pinid**は KSCAMERA\_extendedprop\_filterscope に設定されます。

プロパティコントロールは、同期または非同期のいずれかです。 コントロールが同期されている場合は、KSCAMERA\_EXTENDEDPROP\_CAPS\_ASYNCCONTROL フラグが**機能**に設定されます。 また、コントロールがキャンセル可能な場合、**機能**メンバーには、KSCAMERA\_extendedprop\_CAPS\_キャンセル可能なフラグが含まれます。

ペイロードサイズは、サイズメンバーで設定されます。 **Size**の値は、ペイロード全体のサイズです。 プロパティがヘッダーのみを使用する場合は、 **Size** = **sizeof**(KSCAMERA\_extendedprop\_header) になります。 それ以外**の場合は、**  = **sizeof**(KSCAMERA\_extendedprop\_HEADER) + **sizeof**(特定のデータの制御) を指定します。

## <a name="control-specific-data"></a>特定のデータの制御


一部のプロパティコントロールは、追加のデータを保持するために追加の構造体を使用します。 1つのデータ値が使用される場合、プロパティデータには、 [**KSCAMERA\_extendedprop\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の後に、 [**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)構造体が含まれます。 **KSCAMERA\_EXTENDEDPROP\_値**構造体を使用すると、プロパティは、複数のデータ型の1つとして1つの値を表すことができます。

追加のデータを取得または設定するために、プロパティは、 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の後に独自の特殊なデータ構造を持ちます。 次の例では、ksk プロパティ[ **\_CAMERACONTROL\_EXTENDED\_FIELDOFVIEW**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-fieldofview)プロパティの\_GET 要求である、KSPROPERTY プロパティのプロパティ固有のデータを設定するドライバーコードフラグメントを示します。

```cpp
#define FL_WIDE_ANGLE 35
#define FL_NORMAL     50

PBYTE Payload = (PBYTE)PropData;
PKSCAMERA_EXTENDEDPROP_HEADER ExtendedPropHeader = (PKSCAMERA_EXTENDEDPROP_HEADER)Payload;
PKSCAMERA_EXTENDEDPROP_FIELDOFVIEW ExtendedDataFov = (PKSCAMERA_EXTENDEDPROP_FIELDOFVIEW)(Payload + sizeof(KSCAMERA_EXTENDEDPROP_HEADER));

ExtendedPropHeader->Version = 1;
ExtendedPropHeader->PinId = KSCAMERA_EXTENDEDPROP_FILTERSCOPE;
ExtendedPropHeader->Size = sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_FIELDOFVIEW);
ExtendedPropHeader->Result = 0;
ExtendedPropHeader->Flags = 0;
ExtendedPropHeader->Capability = 0;

ExtendedDataFov->NormalizedFocalLengthX = FL_WIDE_ANGLE;
ExtendedDataFov->NormalizedFocalLengthY = FL_WIDE_ANGLE;
ExtendedDataFov->Flag = 0;
ExtendedDataFov->Reserved = 0;
```

 

 




