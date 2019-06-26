---
title: MSFC\_HbaApiVersion WMI クラス
description: MSFC\_HbaApiVersion WMI クラス
ms.assetid: 642b8313-d1ca-4c07-9c39-b49ef65b4438
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4a97e2579f71f20e8f26999eb97d26f356e81915
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384151"
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

[**MSFC\_HbaApiVersion**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff562507(v=vs.85))

この WMI クラスに関連付けられているメソッドはありません。

 

 





