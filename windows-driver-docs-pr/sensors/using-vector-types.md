---
title: ベクター型センサーを使用します。
description: ベクター型センサーを使用します。
ms.assetid: cadc2cd3-10aa-4a4a-926f-edc01b046f27
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 621a63f0d81101bc8fca0fd9ddc0d3a4b685b42b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557081"
---
# <a name="using-vector-types-with-sensors"></a>ベクター型センサーを使用します。


いくつかのプロパティとデータ フィールドには、情報の配列が含まれます。 センサーなど\_プロパティ\_LIGHT\_応答\_曲線プロパティには 4 バイト符号なし整数の配列が含まれています。 ただし、アプリケーションでは、センサー API を介してこのような配列を受け取る、ときに常に表される VT の種類として\_ベクター |UI1、1 バイト文字の配列。

対象のプロパティとデータのフィールドは配列を含むについては、次を参照してください。[定数](about-sensor-constants.md)します。

次のコード例を作成する方法を示しています、 [IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)センサーの値を格納しているオブジェクト\_プロパティ\_LIGHT\_応答\_曲線。 M という名前の変数\_pSensorProperties はへのポインター、 [IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)インターフェイス。

```cpp
UINT responseCurve[10] = {0}; // Array to contain the response curve data.
// ****************************************************************************************
// The response curve consists of an array of byte pairs.
// The first byte contains the percentage brightness offset to be applied to the display.
// The second byte contains the corresponding ambient light value (in LUX).
// ****************************************************************************************
// (0, 10)
responseCurve[0] = 0; responseCurve[1] = 10;
// (10, 40)
responseCurve[2] = 10; responseCurve[3] = 40;
// (40, 80)
responseCurve[4] = 40; responseCurve[5] = 80;
// (68, 100)
responseCurve[6] = 68; responseCurve[7] = 100;
// (90, 150)
responseCurve[8] = 90; responseCurve[9] = 150;

// Create the buffer.
PROPVARIANT pvCurve = {0};
InitPropVariantFromBuffer(responseCurve, 10 * sizeof (UINT), &pvCurve);

// Add the values to the IPortableDeviceValues object.
hr = m_pSensorProperties->SetValue(SENSOR_PROPERTY_LIGHT_RESPONSE_CURVE, &pvCurve);

PropVariantClear(&pvCurve);
```

## <a name="related-topics"></a>関連トピック
[センサー地理位置情報ドライバー サンプル](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)



