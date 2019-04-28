---
title: MSFC\_FibrePortHBAMethods WMI クラス
description: MSFC\_FibrePortHBAMethods WMI クラス
ms.assetid: 7c9f5c94-0c50-4a7a-b05e-41e93409d1e3
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a34c437755478a3ef9d6ed145daccee9b43960e4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362272"
---
# <a name="msfcfibreporthbamethods-wmi-class"></a>MSFC\_FibrePortHBAMethods WMI クラス


## <span id="ddk_msfc_fibreporthbamethods_wmi_class_kr"></span><span id="DDK_MSFC_FIBREPORTHBAMETHODS_WMI_CLASS_KR"></span>


T11 委員会をサポートする HBA ミニポート ドライバー*ファイバー チャネル HBA API*仕様では、MSFC\_FibrePortHBAMethods クラス ファイバー チャネル ポートで実行できる操作を公開します。 このクラスは、1 つのメソッドを定義します**resetstatistics です**:

```cpp
class MSFC_FibrePortHBAMethods
{
    [key] 
    string InstanceName;
    boolean Active;
    [ Implemented, WmiMethodId(1)]
    void ResetStatistics();
};
```

**Resetstatistics です**メソッドに入力または出力バッファーが必要ありません。 ミニポート ドライバーでは、ポートの統計をリセットするこのメソッドで必要なものを行う必要があります。 このクラスの各ポートの 1 つのインスタンスが必要です。

 

 





