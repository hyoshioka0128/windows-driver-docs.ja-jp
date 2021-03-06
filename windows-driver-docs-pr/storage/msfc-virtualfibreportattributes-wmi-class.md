---
title: MSFC\_VirtualFibrePortAttributes WMI クラス
description: MSFC\_VirtualFibrePortAttributes WMI クラス
ms.assetid: D605D63F-0EBF-44C0-8ADE-729F2DE48487
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fea9070d809025aa05047279a2f42e82253e820f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376705"
---
# <a name="msfcvirtualfibreportattributes-wmi-class"></a>MSFC\_VirtualFibrePortAttributes WMI クラス


WMI クライアントが使用、MSFC\_VirtualFibrePortAttributes クラスの仮想ポートのプロパティを取得します。

MSFC\_VirtualFibrePortAttributes クラスが次のように定義されている*Npivwmi.mof*:

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

WMI ツール スイートによってコンパイルされると、このクラスの定義には、次のデータ構造が生成されます。

[**MSFC\_VirtualFibrePortAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/npivwmi/ns-npivwmi-_msfc_virtualfibreportattributes)

この WMI クラスに関連付けられているメソッドはありません。

 

 





