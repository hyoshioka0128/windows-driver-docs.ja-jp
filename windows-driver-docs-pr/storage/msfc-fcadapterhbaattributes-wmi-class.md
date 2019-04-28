---
title: MSFC\_FCAdapterHBAAttributes WMI クラス
description: MSFC\_FCAdapterHBAAttributes WMI クラス
ms.assetid: fa0ff9c2-e7cc-4000-bd18-ade953e57dcc
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 49de9254ff7d685068ae3fbff008bcfca09f638e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360889"
---
# <a name="msfcfcadapterhbaattributes-wmi-class"></a>MSFC\_FCAdapterHBAAttributes WMI クラス


## <span id="ddk_msfc_fcadapterhbaattributes_wmi_class_kr"></span><span id="DDK_MSFC_FCADAPTERHBAATTRIBUTES_WMI_CLASS_KR"></span>


T11 委員会をサポートする HBA ミニポート ドライバー*ファイバー チャネル HBA API*仕様では、MSFC\_FCAdapterHBAAttributes WMI クラス、ファイバー チャネル アダプターに関連付けられている属性の情報を公開します。

MSFC\_FCAdapterHBAAttributes クラスが次のように定義されている*Hbaapi.mof*:

```cpp
class MSFC_FCAdapterHBAAttributes {
  [key] 
  string InstanceName;
  boolean Active;
  [Description ("Unique identifier for the adapter. This"
                "identifier must be unique among all"
                "adapters. The same value for the "
                "identifier must be used for the same"
                "adapter in other classes that expose"
                "adapter information") : amended,
   WmiRefClass("MSFC_FibreChannelAdapter"),
   WmiRefProperty("UniqueAdapterId"),
   WmiDataId(1)] uint64  UniqueAdapterId;
  [HBA_STATUS_QUALIFIERS, WmiDataId(2)] HBA_STATUS HBAStatus;
  [HBAType("HBA_WWN"),WmiDataId(3)] uint8  NodeWWN[8];
  [WmiDataId(4)] uint32  VendorSpecificID;
  [WmiDataId(5)] uint32 NumberOfPorts;
  [WmiDataId(6)] string  Manufacturer;
  [MaxLen(64), WmiDataId(7)] string SerialNumber; 
  [MaxLen(256), WmiDataId(8)] string Model; 
  [MaxLen(256), WmiDataId(9)] string ModelDescription; 
  [MaxLen(256), WmiDataId(10)] string NodeSymbolicName; 
  [MaxLen(256), WmiDataId(11)] string HardwareVersion; 
  [MaxLen(256), WmiDataId(12)] string DriverVersion; 
  [MaxLen(256), WmiDataId(13)] string OptionROMVersion; 
  [MaxLen(256), WmiDataId(14)] string FirmwareVersion; 
  [MaxLen(256), WmiDataId(15)] string DriverName; 
  [MaxLen(256), WmiDataId(16)] string MfgDomain;
};
```

WMI ツール スイートによってコンパイルされるときに、このクラスの定義には、次のデータ構造が生成されます。

[**MSFC\_FCAdapterHBAAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff562495)

この WMI クラスに関連付けられているメソッドはありません。

 

 





