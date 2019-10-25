---
title: MSFC\_FC4STATISTICS WMI クラス
description: MSFC\_FC4STATISTICS WMI クラス
ms.assetid: 49cd4104-1fe8-46ec-9216-c5c078666c02
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b262a64b51adba4c8afa36a9f86aad3da0163c61
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842865"
---
# <a name="msfc_fc4statistics-wmi-class"></a>MSFC\_FC4STATISTICS WMI クラス


## <span id="ddk_msfc_fc4statistics_wmi_class_kr"></span><span id="DDK_MSFC_FC4STATISTICS_WMI_CLASS_KR"></span>


T11 委員会の*ファイバーチャネル HBA API*仕様をサポートする hba ミニポートドライバーは、msfc\_FC4STATISTICS WMI クラスを使用して、指定された FC-4 プロトコルの種類が Nx\_port のトラフィック統計を、[**GetFC4Statistics**](getfc4statistics.md) WMI メソッドを呼び出します。

MSFC\_FC4STATISTICS クラスは、次のように*Hbaapi .mof*で定義されます。

```cpp
class MSFC_FC4STATISTICS {
  [WmiDataId(1)] uint64  InputRequests;
  [WmiDataId(2)] uint64  OutputRequests;
  [WmiDataId(3)] uint64  ControlRequests;
  [WmiDataId(4)] uint64  InputMegabytes;
  [WmiDataId(5)] uint64  OutputMegabytes;
};
```

WMI ツールスイートによってコンパイルされた場合、このクラス定義では次のデータ構造が生成されます。

[**MSFC\_FC4STATISTICS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_fc4statistics)

この WMI クラスに関連付けられているメソッドはありません。

 

 





