---
title: MSFC\_FC4STATISTICS WMI クラス
description: MSFC\_FC4STATISTICS WMI クラス
ms.assetid: 49cd4104-1fe8-46ec-9216-c5c078666c02
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f22986aa6596dc737489bd6b25e1d824307efcdd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550301"
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

[**MSFC\_FC4STATISTICS**](https://msdn.microsoft.com/library/windows/hardware/ff562492)

この WMI クラスに関連付けられているメソッドはありません。

 

 





