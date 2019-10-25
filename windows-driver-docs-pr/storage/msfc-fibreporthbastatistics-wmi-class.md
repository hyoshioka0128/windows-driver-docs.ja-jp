---
title: MSFC\_FibrePortHBAStatistics WMI クラス
description: MSFC\_FibrePortHBAStatistics WMI クラス
ms.assetid: 24c787b6-b9f7-4c9b-8d1d-6b2796f65622
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 91e67801cd058a2cd88a8a8dac3b3f0c32d0bbb4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826164"
---
# <a name="msfc_fibreporthbastatistics-wmi-class"></a>MSFC\_FibrePortHBAStatistics WMI クラス


## <span id="ddk_msfc_fibreporthbastatistics_wmi_class_kr"></span><span id="DDK_MSFC_FIBREPORTHBASTATISTICS_WMI_CLASS_KR"></span>


WMI クライアントは、MSFC\_FibrePortHBAStatistics クラスを使用して、hba のポートに関連する統計を HBA ミニポートドライバーに照会します。 MSFC\_FibrePortHBAStatistics クラスは、 [msfc\_HBAPORTSTATISTICS WMI クラス](msfc-hbaportstatistics-wmi-class.md)のすべての情報に加え、ポートのいくつかの識別子情報を報告します。

MSFC\_FibrePortHBAStatistics クラスは、次のように*Hbaapi .mof*で定義されます。

```cpp
class MSFC_FibrePortHBAStatistics
{
    [key] 
    string InstanceName;
    boolean Active;
    [
     Description ("Unique identifier for the port. "
                   "This identifier must be unique "
                   "among all ports on all adapters."
                   "The same value for the identifier "
                   "must be used for the same port "
                   "in other classes that expose port "
                   "information") : amended,
     WmiRefClass("MSFC_FibrePort"),
     WmiRefProperty("UniquePortId"),
     WmiDataId(1)
    ]
    uint64 UniquePortId;
    [WmiDataId(2),
     HBA_STATUS_QUALIFIERS
    ]
    uint32 HBAStatus;
    // Note 4 byte padding
    [ WmiDataId(3) ]
    MSFC_HBAPortStatistics Statistics;
};
```

WMI ツールスイートによってコンパイルされた場合、このクラス定義では次のデータ構造が生成されます。

[**MSFC\_FibrePortHBAStatistics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_fibreporthbastatistics)

この WMI クラスに関連付けられているメソッドはありません。

 

 





