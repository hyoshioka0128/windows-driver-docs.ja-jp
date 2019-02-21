---
title: MSFC\_AdapterEvent WMI クラス
description: MSFC\_AdapterEvent WMI クラス
ms.assetid: 83077288-e3f6-4b21-80ed-677aad7d2979
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0218dfb72fb0cac509ed9debbefc96982af765fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527307"
---
# <a name="msfcadapterevent-wmi-class"></a>MSFC\_AdapterEvent WMI クラス


## <span id="ddk_msfc_adapterevent_wmi_class_kr"></span><span id="DDK_MSFC_ADAPTEREVENT_WMI_CLASS_KR"></span>


T11 委員会をサポートする HBA ミニポート ドライバー*ファイバー チャネル HBA API*仕様では、MSFC\_AdapterEvent クラスになるように登録が WMI クライアント アダプターのイベントの特性を報告するにはこれらのイベントの通知。

MSFC\_AdapterEvent クラスが次のように定義されている*Hbaapi.mof*:

```cpp
class MSFC_AdapterEvent : WMIEvent  {
  [key] string InstanceName; boolean  Active;
  [WmiDataId(1), Description("Event Type") : amended, 
    _TYPE_QUALIFIERS] uint32  EventType;
  [WmiDataId(2), Description("Adapter WWN") : amended, 
    ("HBA_WWN")] uint8  PortWWN[8];
};
```

WMI ツール スイートによってコンパイルされるときに、このクラスの定義には、次のデータ構造が生成されます。

[**MSFC\_AdapterEvent**](https://msdn.microsoft.com/library/windows/hardware/ff562475)

この WMI クラスに関連付けられているメソッドはありません。

 

 





