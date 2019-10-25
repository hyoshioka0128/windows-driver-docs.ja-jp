---
title: MSFC\_VirtualFibrePortAttributes WMI クラス
description: MSFC\_VirtualFibrePortAttributes WMI クラス
ms.assetid: D605D63F-0EBF-44C0-8ADE-729F2DE48487
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 34206f03a4fed727db95338b47d577eed4385164
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845598"
---
# <a name="msfc_virtualfibreportattributes-wmi-class"></a>MSFC\_VirtualFibrePortAttributes WMI クラス


WMI クライアントは、MSFC\_VirtualFibrePortAttributes クラスを使用して、仮想ポートのプロパティを取得します。

MSFC\_VirtualFibrePortAttributes クラスは、 *Npivwmi*で次のように定義されています。

```mof
class MSFC_VirtualFibrePortAttributes  
{  
    [WmiDataId(1), Description("Status of the virtual port"):Amended,  
    uint32 Status;  
  
    [WmiDataId(2), Description("FC Id"):Amended]  
    uint32 FCId;  
      
    [WmiDataId(3), Description("Port symbolic name"):Amended]  
    uint16 VirtualName[64];  
  
    [WmiDataId(4), Description("An opaque tag passed in by the app. 128 bit so that a guid can be stored in it."):Amended]  
    uint8 Tag[16];  
  
    [WmiDataId(5), Description("The world wide port name of the virtual port"):Amended]  
    uint8 WWPN[8];   
  
    [WmiDataId(6), Description("The world wide node name of the virtual port"):Amended]  
    uint8 WWNN[8];   
  
    [WmiDataId(7), Description("The world wide node name of fabric"):Amended]  
    uint8 FabricWWN[8];  
};  
```

このクラス定義は、WMI ツールスイートによってコンパイルされると、次のデータ構造を生成します。

[**MSFC\_VirtualFibrePortAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/npivwmi/ns-npivwmi-_msfc_virtualfibreportattributes)

この WMI クラスに関連付けられているメソッドはありません。

 

 





