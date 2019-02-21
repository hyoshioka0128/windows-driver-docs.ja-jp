---
title: 環境光センサーをサポートしています。
description: 環境光センサーをサポートしています。
ms.assetid: a0875084-c093-4659-91b9-375450f65234
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5b2eb7bf2c72f0e5e4e73c29f74050a19917ff3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538710"
---
# <a name="supporting-ambient-light-sensors"></a>環境光センサーをサポートしています。


環境光センサーは、現在の照明条件を測定できます。 光センサーからデータを使用して、画面の明るさとキーボードの照明を自動的に調整することができます。 照明条件を現在のユーザー インターフェイス要素を調整する光対応のアプリケーションを作成することもできます。 Windows 8 では環境光センサー (適応型輝度調整) を持つ自動明るさコントロールがサポートされます。

Windows 8 には両方の ACPI 3.0b クラス ドライバーのサポートが含まれています-準拠と HID 準拠の環境光センサーの実装。 これは、環境光センサーをサポートするためにカスタム ドライバーを記述する必要はないことを意味します。 これらのドライバーが Windows Sensor and Location プラットフォームと統合するため、これらのセンサーも、センサー API ベースのクライアント アプリケーションで使用できます。

環境光センサーと Windows 8 での適応型輝度調整機能の詳細についてを参照してください「の統合環境光センサーを Windows 10」ホワイト ペーパー、 [Windows ハードウェア デベロッパー センター](https://docs.microsoft.com/windows-hardware/design/whitepapers/integrating-ambient-light-sensors-with-computers-running-windows-10-creators-update) web サイト。

ACPI 3.0b ではない環境光センサー用に準拠している、または HID 準拠、Sensor and Location プラットフォームに統合するためのセンサー ドライバーを作成する必要があります。

## <a name="handling-light-sensor-properties"></a>光センサー プロパティの処理


Windows 8 では、センサーの種類が正しい\_データ\_型\_LIGHT\_レベル\_LUX は VT\_R4。 ただし、Windows 7 では、適切な型が、VT\_UI4 します。 その結果、デバイス ドライバーは、両方の種類を正しく処理する必要があります。

Windows 8 および Windows 7 の相違点の別のポイントは、以前の ALS デバイス ドライバーがセンサーを想定している\_プロパティ\_変更\_と小文字の区別、内の値のセットとしてではなく、1つの値として渡される**IPortableDeviceValues**オブジェクト。

次の擬似コードは、センサーの使用可能な型の適切な処理を示しています。\_データ\_型\_LIGHT\_レベル\_LUX します。

```cpp
SetLuxChangeSensitivity(PROPVARIANT var)
{
    if (var.vt == VT_UNKNOWN)
    {
        CComPtr<IPortableDeviceValues> spValues;
        PROPVARIANT entry;

        //
        // Var is a pointer to an IPortableDeviceValues
        // container. Cast and iterate through its entries.
        //

        spValues = static_cast<IPortableDeviceValues*>(pVar->punkVal);

        foreach entry in spValues
        {
            //
            // Note: omitting check for SENSOR_DATA_TYPE_LIGHT_LEVEL_LUX key
            //

            if (entry.vt == VT_R4)
            {
                //
                // VT_R4 is the expected type for
                // SENSOR_DATA_TYPE_LIGHT_LEVEL_LUX.
                // Reference entry.fltVal.
                //
            }
            else if (entry.vt == VT_UI4)
            {
                //
                // VT_UI4 is deprecated, but use it anyway.
                // Reference entry.ulVal.
                //
            }
            else
            {
                //
                // All other types are invalid.
                // Return an error accordingly.
                //
            }
        }
    }
    else if (var.vt == VT_UI4)
    {
        //
        // Top level type of VT_UI4 is deprecated for
        // SENSOR_PROPERTY_CHANGE_SENSITIVITY, but use it anyway.
        // Reference entry.ulVal.
        //
    }
    else
    {
        //
        // All other types are invalid.
        // Return an error accordingly.
        //
    }
}
```

## <a name="related-topics"></a>関連トピック

[センサー ドライバー開発の基本概念](sensor-driver-development-basics.md)



