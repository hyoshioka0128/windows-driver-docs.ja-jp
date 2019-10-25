---
title: MSFC\_NPIVLUNMappingInformation WMI クラス
description: MSFC\_NPIVLUNMappingInformation WMI クラス
ms.assetid: F8BCDEDE-5EF3-464D-8592-5DF1878D3694
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 62875ed4b850796bd6bc7d0918a5d3d0832e4c7d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824258"
---
# <a name="msfc_npivlunmappinginformation-wmi-class"></a>MSFC\_NPIVLUNMappingInformation WMI クラス


WMI クライアントは、MSFC\_LUNMappingInformation クラスを使用して、LUN を仮想ポートマッピング情報に取得します。

MSFC\_NPIVLUNMappingInformation クラスは、 *Npivwmi*で次のように定義されています。

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

このクラス定義は、WMI ツールスイートによってコンパイルされると、次のデータ構造を生成します。

[**MSFC\_NPIVLUNMappingInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/npivwmi/ns-npivwmi-_msfc_npivlunmappinginformation)

この WMI クラスに関連付けられているメソッドはありません。

 

 





