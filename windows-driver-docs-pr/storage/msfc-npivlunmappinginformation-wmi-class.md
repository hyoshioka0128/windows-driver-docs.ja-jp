---
title: MSFC\_NPIVLUNMappingInformation WMI クラス
description: MSFC\_NPIVLUNMappingInformation WMI クラス
ms.assetid: F8BCDEDE-5EF3-464D-8592-5DF1878D3694
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 67a72fc8ba7a6f8005b3be662b2d96e35cd29ace
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376734"
---
# <a name="msfcnpivlunmappinginformation-wmi-class"></a>MSFC\_NPIVLUNMappingInformation WMI クラス


WMI クライアントが使用、MSFC\_LUNMappingInformation クラスは、LUN を仮想ポートのマッピング情報を取得します。

MSFC\_NPIVLUNMappingInformation クラスが次のように定義されている*Npivwmi.mof*:

```mof
class MSFC_NPIVLUNMappingInformation  
{  
    [WmiDataId(1), Description("The world wide port name of the virtual port"):Amended]  
     uint8 WWPNVirtualPort[8];  
  
    [WmiDataId(2), Description("The world wide port name of the physical port"):Amended]  
    uint8 WWPNPhysicalPort[8];  
  
    [WmiDataId(3),  
    read  
    ] uint8 OSBus;  
  
    [WmiDataId(4),  
    read  
    ] uint8 OSTarget;  
  
    [WmiDataId(5),  
    read  
    ] uint8 OSLUN;  
};  
```

WMI ツール スイートによってコンパイルされると、このクラスの定義には、次のデータ構造が生成されます。

[**MSFC\_NPIVLUNMappingInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/npivwmi/ns-npivwmi-_msfc_npivlunmappinginformation)

この WMI クラスに関連付けられているメソッドはありません。

 

 





