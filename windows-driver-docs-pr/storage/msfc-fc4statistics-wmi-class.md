---
title: MSFC\_FC4STATISTICS WMI クラス
description: MSFC\_FC4STATISTICS WMI クラス
ms.assetid: 49cd4104-1fe8-46ec-9216-c5c078666c02
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bc0c79fcdb0d4367e635ed69e0d9713aec7edb83
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377518"
---
# <a name="msfcfc4statistics-wmi-class"></a>MSFC\_FC4STATISTICS WMI クラス


## <span id="ddk_msfc_fc4statistics_wmi_class_kr"></span><span id="DDK_MSFC_FC4STATISTICS_WMI_CLASS_KR"></span>


T11 委員会をサポートする HBA ミニポート ドライバー*ファイバー チャネル HBA API*仕様では、MSFC\_Nx の種類のポートでトラフィック統計情報を報告する FC4STATISTICS WMI クラス\_のポート、FC 4 プロトコルへの呼び出しに応答で示される、 [ **GetFC4Statistics** ](getfc4statistics.md) WMI メソッド。

MSFC\_FC4STATISTICS クラスが次のように定義されている*Hbaapi.mof*:

```cpp
class MSFC_FC4STATISTICS {
  [WmiDataId(1)] uint64  InputRequests;
  [WmiDataId(2)] uint64  OutputRequests;
  [WmiDataId(3)] uint64  ControlRequests;
  [WmiDataId(4)] uint64  InputMegabytes;
  [WmiDataId(5)] uint64  OutputMegabytes;
};
```

WMI ツール スイートによってコンパイルされるときに、このクラスの定義には、次のデータ構造が生成されます。

[**MSFC\_FC4STATISTICS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_msfc_fc4statistics)

この WMI クラスに関連付けられているメソッドはありません。

 

 





