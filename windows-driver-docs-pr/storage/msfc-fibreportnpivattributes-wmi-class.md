---
title: MSFC\_FibrePortNPIVAttributes WMI クラス
description: MSFC\_FibrePortNPIVAttributes WMI クラス
ms.assetid: A778E00A-476C-4763-B652-3312B7913F9C
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2b2df992d966c401eb5f3e1c18b40c927538413e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382557"
---
# <a name="msfcfibreportnpivattributes-wmi-class"></a>MSFC\_FibrePortNPIVAttributes WMI クラス


WMI クライアントが使用、MSFC\_FibrePortNPIVAttributes クラス仮想ポートを物理ポートの作成に関する情報を取得します。

MSFC\_FibrePortNPIVAttributes クラスが次のように定義されている*Npivwmi.mof*:

```mof
class MSFC_FibrePortNPIVAttributes   
{  
    [WmiDataId(1), Description("The world wide port name of the physical port"):Amended]  
     uint8 WWPN[8];   
  
    [WmiDataId(2), Description("The world wide node name of the physical port"):Amended]  
     uint8 WWNN[8];   
  
    [WmiDataId(3),  
     read,  
     Description("Number of virtual ports on this adapter."):Amended  
    ]uint32 NumberVirtualPorts;  
  
     [WmiDataId(4),  
      read,  
      Description("Array of virtual ports."):Amended,
      WmiSizeIs("NumberVirtualPorts")  
     ]  
     MSFC_VirtualFibrePortAttributes VirtualPorts[];  
};
```

WMI ツール スイートによってコンパイルされると、このクラスの定義には、次のデータ構造が生成されます。

[**MSFC\_FibrePortNPIVAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/npivwmi/ns-npivwmi-_msfc_fibreportnpivattributes)

この WMI クラスに関連付けられているメソッドはありません。

 

 





