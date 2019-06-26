---
title: MS\_SM\_HbaApiVersion WMI クラス
description: MS\_SM\_HbaApiVersion WMI クラス
ms.assetid: 3d0591e5-ed95-4509-bd27-e122ac9186d2
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 506a8bf306764bbbbd10db0b163e3caf1696f43f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386141"
---
# <a name="mssmhbaapiversion-wmi-class"></a>MS\_SM\_HbaApiVersion WMI クラス


記憶域管理 API をサポートする HBA ミニポート ドライバーは、MS を使用して\_SM\_HbaApiVersion クラスは、現在の HBA の API バージョン。

MS\_SM\_HbaApiVersion クラスが次のように定義されている*Hbaapi.mof*:

```cpp
class MS_SM_HbaApiVersion
{
    uint32 WmiHbaApiVersion;  
    uint32 HbaApiVersion;  
    string Description;
};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SM\_HbaApiVersion**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563211(v=vs.85))

この WMI クラスに関連付けられているメソッドはありません。

 

 





