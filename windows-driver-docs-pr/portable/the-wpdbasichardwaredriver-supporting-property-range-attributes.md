---
Description: プロパティ範囲属性のサポート
title: プロパティ範囲属性のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 692759b656b8e2cfd10c8a29910492772413b39c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387303"
---
# <a name="supporting-the-property-range-attributes"></a>プロパティ範囲属性のサポート


サンプル ドライバーは、2 つのプロパティをサポートしています。 更新間隔 (センサー\_更新\_間隔) と現在のセンサーの読み取り (センサー\_読み取り)。 これらの各プロパティには、一般的な属性 (探し、削除、読み取り可能な書き込み可能なおよびなど) のセットをサポートしています。 さらに、これらのプロパティは、特定の範囲の属性 (最小、最大、およびステップ値) をサポートします。

センサーの読み取りの場合は、プロパティは、範囲で表されます (WPD\_プロパティ\_属性\_フォーム\_範囲)。

プロパティ属性内のエントリに対応して、 *Rs232connection.h*ファイル。 これらのエントリは、アプリケーションが特定の範囲内のプロパティを設定するときに使用できる手順の値と、デバイスをサポートする最小値と最大値を指定します。

```cpp
#define SENSOR_READING_MIN 1  
#define SENSOR_READING_MAX 378  
#define SENSOR_READING_STEP 1   
```

これらの属性の範囲を設定するコードが WpdObjectProperties::GetPropertyAttributesForObject で見つかった (で、 *Wpdobjectproperties.cpp*モジュール)。 このコードで定義されている値を使用して*Rs232connection.h*これらの属性を設定します。

```cpp
else if (IsEqualPropertyKey(Key, SENSOR_READING))
{
    // Form range attributes for the temperature reading property
    hr = pAttributes->SetUnsignedIntegerValue(WPD_PROPERTY_ATTRIBUTE_FORM, 
                                              WPD_PROPERTY_ATTRIBUTE_FORM_RANGE);
    CHECK_HR(hr, 
             "Failed to set WPD_PROPERTY_ATTRIBUTE_RANGE_MIN 
              for SENSOR_READING");

    hr = pAttributes->SetUnsignedIntegerValue(WPD_PROPERTY_ATTRIBUTE_RANGE_MIN, 
                                              SENSOR_READING_MIN);
    CHECK_HR(hr, 
             "Failed to set WPD_PROPERTY_ATTRIBUTE_RANGE_MIN 
              for SENSOR_READING");

    hr = pAttributes->SetUnsignedIntegerValue(WPD_PROPERTY_ATTRIBUTE_RANGE_MAX, 
                                              SENSOR_READING_MAX);
    CHECK_HR(hr, 
             "Failed to set WPD_PROPERTY_ATTRIBUTE_RANGE_MAX 
              for SENSOR_READING");

    hr = pAttributes->SetUnsignedIntegerValue(WPD_PROPERTY_ATTRIBUTE_RANGE_STEP, 
                                              SENSOR_READING_STEP);
    CHECK_HR(hr, 
             "Failed to set WPD_PROPERTY_ATTRIBUTE_RANGE_STEP 
              for TEMPERATURE_SENSOR_READING");
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





