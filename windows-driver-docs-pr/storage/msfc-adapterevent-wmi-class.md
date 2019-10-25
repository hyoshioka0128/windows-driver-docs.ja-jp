---
title: MSFC\_AdapterEvent WMI クラス
description: MSFC\_AdapterEvent WMI クラス
ms.assetid: 83077288-e3f6-4b21-80ed-677aad7d2979
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 616383dd556c31ed0508ac0edb4c30dfb0f54f6f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844520"
---
# <a name="msfc_adapterevent-wmi-class"></a>MSFC\_AdapterEvent WMI クラス


## <span id="ddk_msfc_adapterevent_wmi_class_kr"></span><span id="DDK_MSFC_ADAPTEREVENT_WMI_CLASS_KR"></span>


T11 委員会の*ファイバーチャネル HBA API*仕様をサポートする hba ミニポートドライバーは、msfc\_adapterevent クラスを使用して、これらのイベントの通知を受け取るように登録されている WMI クライアントにアダプターイベントの特性を報告します。

MSFC\_AdapterEvent クラスは、 *Hbaapi .mof*で次のように定義されています。

```cpp
class MSFC_AdapterEvent : WMIEvent  {
  [key] string InstanceName; boolean  Active;
  [WmiDataId(1), Description("Event Type") : amended, 
    _TYPE_QUALIFIERS] uint32  EventType;
  [WmiDataId(2), Description("Adapter WWN") : amended, 
    ("HBA_WWN")] uint8  PortWWN[8];
};
```

WMI ツールスイートによってコンパイルされた場合、このクラス定義では次のデータ構造が生成されます。

[**MSFC\_AdapterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_adapterevent)

この WMI クラスに関連付けられているメソッドはありません。

 

 





