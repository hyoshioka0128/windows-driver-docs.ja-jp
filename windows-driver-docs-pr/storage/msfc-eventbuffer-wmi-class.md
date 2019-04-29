---
title: MSFC\_EventBuffer WMI クラス
description: MSFC\_EventBuffer WMI クラス
ms.assetid: ce16e42c-5d0b-47e9-9baa-53dcec482940
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3665c95af6708bd9f0df839dbe42398d85c65adb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325950"
---
# <a name="msfceventbuffer-wmi-class"></a>MSFC\_EventBuffer WMI クラス


## <span id="ddk_msfc_eventbuffer_wmi_class_kr"></span><span id="DDK_MSFC_EVENTBUFFER_WMI_CLASS_KR"></span>


T11 委員会をサポートする HBA ミニポート ドライバー*ファイバー チャネル HBA API*仕様では、MSFC\_アダプター イベント データがこれらの通知に登録されている WMI クライアントをレポートする EventBuffer クラスイベント。

MSFC\_EventBuffer クラスが次のように定義されている*Hbaapi.mof*:

```cpp
class MSFC_EventBuffer { 
  [WmiDataId(1)] uint32  EventType;
  [WmiDataId(2)] uint32  EventInfo[4];
};
```

WMI ツール スイートによってコンパイルされるときに、このクラスの定義には、次のデータ構造が生成されます。

[**MSFC\_EventBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff562480)

この WMI クラスに関連付けられているメソッドはありません。

 

 





