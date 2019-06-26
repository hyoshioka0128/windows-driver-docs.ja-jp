---
title: MSFC\_EventBuffer WMI クラス
description: MSFC\_EventBuffer WMI クラス
ms.assetid: ce16e42c-5d0b-47e9-9baa-53dcec482940
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e2e5d5d82aefc63473bdeda72ae1041f7a43f6cf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371161"
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

[**MSFC\_EventBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_msfc_eventbuffer)

この WMI クラスに関連付けられているメソッドはありません。

 

 





