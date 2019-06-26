---
title: 拡張カメラ コントロール ペイロード
description: KSPROPERTYSETID_ExtendedCameraControl プロパティ セット内のコントロールのプロパティを取得および設定のプロパティのデータの一般的なペイロード形式を使用します。
ms.assetid: 347413DB-229B-40D7-BD3E-931493EE1FBC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81d54c27308b87bb684d89d3b51486361b6fbb2a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384097"
---
# <a name="extended-camera-control-payloads"></a>拡張カメラ コントロール ペイロード


内のコントロールのプロパティ、 [KSPROPERTYSETID\_ExtendedCameraControl](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropertysetid-extendedcameracontrol)プロパティ セットを取得および設定のプロパティのデータの一般的なペイロード形式を使用します。

## <a name="extended-camera-property-header"></a>カメラの拡張プロパティのヘッダー


すべてのペイロードが始まり、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造体。 この構造体には、関連付けられたコントロール フラグと機能を使用してピン留めするターゲットが含まれています。 特定のコントロールによって、**機能**メンバーがコントロールによって提供される機能のセットが含まれます。 **フラグ**メンバーは実際の機能を含めることが現在設定またはコントロールに対して設定します。

**PinId**メンバーがカメラの暗証番号 (pin) またはフィルターの暗証番号 (pin) のいずれかであるターゲットを指定します。 フィルター レベルの制御は、プロパティ**PinId** KSCAMERA に設定されている\_EXTENDEDPROP\_FILTERSCOPE します。

プロパティ コントロールは、同期または非同期のどちらかです。 コントロールが、同期の場合、KSCAMERA し\_EXTENDEDPROP\_CAP\_ASYNCCONTROL フラグに設定されて**機能**。 コントロールが、キャンセル可能な場合は、**機能**メンバーには、KSCAMERA が含まれています\_EXTENDEDPROP\_CAP\_キャンセル可能なフラグ。

ペイロードのサイズは、サイズのメンバーで設定されます。 値は、**サイズ**ペイロードの全体サイズです。 プロパティが、ヘッダーのみを使用している場合**サイズ** = **sizeof**(KSCAMERA\_EXTENDEDPROP\_ヘッダー)。 それ以外の場合、**サイズ** = **sizeof**(KSCAMERA\_EXTENDEDPROP\_ヘッダー) + **sizeof**(コントロールの特定のデータ)。

## <a name="control-specific-data"></a>コントロールの特定のデータ


一部のコントロールのプロパティは、追加のデータを保持するために別の構造体を使用します。 1 つのデータ値が使用される場合、プロパティのデータが含まれます、 [ **KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)後構造体[ **KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)します。 **KSCAMERA\_EXTENDEDPROP\_値**構造により、複数のデータ型の 1 つとして、単一の値を表現するプロパティ。

プロパティを取得または追加のデータを設定、独自の特別なデータ構造体の次にあるが、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)します。 次の例を KSPROPERTY のプロパティの特定のデータを設定するドライバーのコード フラグメント\_型\_の GET 要求、 [ **KSPROPERTY\_CAMERACONTROL\_拡張\_FIELDOFVIEW** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-fieldofview)プロパティ。

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

 

 




