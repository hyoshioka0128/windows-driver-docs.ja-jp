---
title: MSFC\_FibrePortNPIVAttributes WMI クラス
description: MSFC\_FibrePortNPIVAttributes WMI クラス
ms.assetid: A778E00A-476C-4763-B652-3312B7913F9C
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a35aa5a94f30d268eb28b510d6ba1d2a2d2352d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826136"
---
# <a name="msfc_fibreportnpivattributes-wmi-class"></a>MSFC\_FibrePortNPIVAttributes WMI クラス


WMI クライアントは、MSFC\_FibrePortNPIVAttributes クラスを使用して、物理ポート用に作成された仮想ポートに関する情報を取得します。

MSFC\_FibrePortNPIVAttributes クラスは、 *Npivwmi*で次のように定義されています。

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

このクラス定義は、WMI ツールスイートによってコンパイルされると、次のデータ構造を生成します。

[**MSFC\_FibrePortNPIVAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/npivwmi/ns-npivwmi-_msfc_fibreportnpivattributes)

この WMI クラスに関連付けられているメソッドはありません。

 

 





