---
title: MS\_SMHBA\_PROTOCOLSTATISTICS WMI クラス
description: MS\_SMHBA\_PROTOCOLSTATISTICS WMI クラス
ms.assetid: 718ae583-254d-4807-b8e2-5eb39017c097
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2b09709ef965b8d88bcc3ce40dd4925230e45c67
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386138"
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

[**MS\_SMHBA\_PROTOCOLSTATISTICS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_ms_smhba_protocolstatistics)

この WMI クラスに関連付けられているメソッドはありません。

 

 





