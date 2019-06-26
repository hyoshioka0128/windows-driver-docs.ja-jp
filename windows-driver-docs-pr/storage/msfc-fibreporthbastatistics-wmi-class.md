---
title: MSFC\_FibrePortHBAStatistics WMI クラス
description: MSFC\_FibrePortHBAStatistics WMI クラス
ms.assetid: 24c787b6-b9f7-4c9b-8d1d-6b2796f65622
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e333ed7bc83204f5ade7990b763937abe817a044
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380601"
---
# <a name="msfcfibreporthbastatistics-wmi-class"></a>MSFC\_FibrePortHBAStatistics WMI クラス


## <span id="ddk_msfc_fibreporthbastatistics_wmi_class_kr"></span><span id="DDK_MSFC_FIBREPORTHBASTATISTICS_WMI_CLASS_KR"></span>


WMI クライアントが使用、MSFC\_クエリ統計の HBA ミニポート ドライバーに FibrePortHBAStatistics クラスの HBA ポートに関連します。 MSFC\_FibrePortHBAStatistics クラスでは、すべての情報の報告、 [MSFC\_HBAPortStatistics WMI クラス](msfc-hbaportstatistics-wmi-class.md)さらに、ポートの場合は、いくつかの識別子情報。

MSFC\_FibrePortHBAStatistics クラスが次のように定義されている*Hbaapi.mof*:

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

WMI ツール スイートによってコンパイルされるときに、このクラスの定義には、次のデータ構造が生成されます。

[**MSFC\_FibrePortHBAStatistics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_msfc_fibreporthbastatistics)

この WMI クラスに関連付けられているメソッドはありません。

 

 





