---
title: MSFC\_EventBuffer WMI クラス
description: MSFC\_EventBuffer WMI クラス
ms.assetid: ce16e42c-5d0b-47e9-9baa-53dcec482940
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f2926ab989023cf44656973b6bf888067e3cd037
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842866"
---
# <a name="msfc_eventbuffer-wmi-class"></a>MSFC\_EventBuffer WMI クラス


## <span id="ddk_msfc_eventbuffer_wmi_class_kr"></span><span id="DDK_MSFC_EVENTBUFFER_WMI_CLASS_KR"></span>


T11 委員会の*ファイバーチャネル HBA API*仕様をサポートする hba ミニポートドライバーは、msfc\_eventbuffer クラスを使用して、これらのイベントの通知を受け取るように登録されている WMI クライアントに、アダプターのイベントデータを報告します。

MSFC\_EventBuffer クラスは、 *Hbaapi .mof*で次のように定義されています。

```cpp
class MSFC_EventBuffer { 
  [WmiDataId(1)] uint32  EventType;
  [WmiDataId(2)] uint32  EventInfo[4];
};
```

WMI ツールスイートによってコンパイルされた場合、このクラス定義では次のデータ構造が生成されます。

[**MSFC\_EventBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_eventbuffer)

この WMI クラスに関連付けられているメソッドはありません。

 

 





