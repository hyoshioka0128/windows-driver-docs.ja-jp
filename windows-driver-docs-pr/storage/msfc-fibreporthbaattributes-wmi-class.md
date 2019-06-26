---
title: MSFC\_FibrePortHBAAttributes WMI クラス
description: MSFC\_FibrePortHBAAttributes WMI クラス
ms.assetid: 028afadf-1a2d-4792-8b6c-d53359af64c1
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e809515b3af709268ddb805bb089e50c62768298
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382553"
---
# <a name="msfcfibreporthbaattributes-wmi-class"></a>MSFC\_FibrePortHBAAttributes WMI クラス


## <span id="ddk_msfc_fibreporthbaattributes_wmi_class_kr"></span><span id="DDK_MSFC_FIBREPORTHBAATTRIBUTES_WMI_CLASS_KR"></span>


FCbre チャネル HBA の API をサポートする HBA ミニポート ドライバーの使用、MSFC\_FibrePortHBAAttributes WMI クラスは、ファイバー チャネル ポートに関連付けられた属性の情報を公開します。 このクラスの各ポートの 1 つのインスタンスが必要です。

MSFC\_FibrePortHBAAttributes クラスが次のように定義されている*Hbaapi.mof*:

```cpp
class MSFC_FibrePortHBAAttributes {
  [key] 
  string InstanceName;
  boolean Active;
  [Description ("Unique identifier for the port. "
    "This identifier must be unique among all "
    "ports on all adapters. The same value for "
    "in other classes that expose port information"
    "the identifier must be used for the same port") : amended,
    WmiRefClass("MSFC_FibrePort"),
    WmiRefProperty("UniquePortId"),
    WmiDataId(1)
    ] uint64 UniquePortId;
  [HBA_STATUS_QUALIFIERS, WmiDataId(2)] HBA_STATUS  HBAStatus;
  [HBAType("HBA_PORTATTRIBUTES"),WmiDataId(3)]
    MSFC_HBAPortAttributesResults Attributes;
};
```

WMI ツール スイートによってコンパイルされるときに、このクラスの定義には、次のデータ構造が生成されます。

[**MSFC\_FibrePortHBAAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_msfc_fibreporthbaattributes)

この WMI クラスに関連付けられているメソッドはありません。

 

 





