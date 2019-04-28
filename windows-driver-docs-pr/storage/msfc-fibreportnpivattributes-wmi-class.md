---
title: MSFC\_FibrePortNPIVAttributes WMI クラス
description: MSFC\_FibrePortNPIVAttributes WMI クラス
ms.assetid: A778E00A-476C-4763-B652-3312B7913F9C
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 490b802bd1634ecb60b2733321c4c54a5b54c6b4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362270"
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

[**MSFC\_FibrePortNPIVAttributes**](https://msdn.microsoft.com/library/windows/hardware/hh127623)

この WMI クラスに関連付けられているメソッドはありません。

 

 





