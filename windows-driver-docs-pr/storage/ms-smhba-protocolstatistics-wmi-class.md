---
title: MS\_SMHBA\_PROTOCOLSTATISTICS WMI クラス
description: MS\_SMHBA\_PROTOCOLSTATISTICS WMI クラス
ms.assetid: 718ae583-254d-4807-b8e2-5eb39017c097
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d9a944f9b572fc5f1b585edeebf45b9c8015e270
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574641"
---
# <a name="mssmhbaprotocolstatistics-wmi-class"></a>MS\_SMHBA\_PROTOCOLSTATISTICS WMI クラス


記憶域管理 API をサポートする HBA ミニポート ドライバーは、MS を使用して\_SMHBA\_トラフィックの統計情報を公開する PROTOCOLSTATISTICS クラス。

MS\_SMHBA\_PROTOCOLSTATISTICS クラスが次のように定義されている*Hbaapi.mof*:

```cpp
class MS_SMHBA_PROTOCOLSTATISTICS
{
    [WmiDataId(1)]
    sint64 SecondsSinceLastReset;

    [WmiDataId(2)]
    sint64 InputRequests;

    [WmiDataId(3)]
    sint64 OutputRequests;

    [WmiDataId(4)]
    sint64 ControlRequests;

    [WmiDataId(5)]
    sint64 InputMegabytes;

    [WmiDataId(6)]
    sint64 OutputMegabytes;
};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SMHBA\_PROTOCOLSTATISTICS**](https://msdn.microsoft.com/library/windows/hardware/ff563172)

この WMI クラスに関連付けられているメソッドはありません。

 

 





