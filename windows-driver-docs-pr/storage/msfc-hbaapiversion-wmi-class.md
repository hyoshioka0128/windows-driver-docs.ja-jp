---
title: MSFC\_HbaApiVersion WMI クラス
description: MSFC\_HbaApiVersion WMI クラス
ms.assetid: 642b8313-d1ca-4c07-9c39-b49ef65b4438
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ff89d0e4041b10e429270db1cbc752b78616ec8c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378982"
---
# <a name="msfchbaapiversion-wmi-class"></a>MSFC\_HbaApiVersion WMI クラス


T11 委員会をサポートする HBA ミニポート ドライバー*ファイバー チャネル HBA API*仕様では、MSFC\_HbaApiVersion クラスは、HBA の API バージョンは現在サポートされています。

MSFC\_HbaApiVersion クラスが次のように定義されている*Hbaapi.mof*:

```cpp
class MSFC_HbaApiVersion
{
    uint32 WmiHbaApiVersion;
    uint32 HbaApiVersion;
    string Description;
};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、次のデータ構造が生成されます。

[**MSFC\_HbaApiVersion**](https://msdn.microsoft.com/library/windows/hardware/ff562507)

この WMI クラスに関連付けられているメソッドはありません。

 

 





