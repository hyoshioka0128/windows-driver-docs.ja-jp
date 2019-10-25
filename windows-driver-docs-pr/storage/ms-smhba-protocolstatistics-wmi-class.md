---
title: MS\_SMHBA\_PROTOCOLSTATISTICS WMI クラス
description: MS\_SMHBA\_PROTOCOLSTATISTICS WMI クラス
ms.assetid: 718ae583-254d-4807-b8e2-5eb39017c097
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e95e12b788a175fc0441e3c1b462527e0e746dd9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844531"
---
# <a name="ms_smhba_protocolstatistics-wmi-class"></a>MS\_SMHBA\_PROTOCOLSTATISTICS WMI クラス


Storage Management API をサポートする HBA ミニポートドライバーは、MS\_SMHBA\_PROTOCOLSTATISTICS クラスを使用して、トラフィックの統計情報を公開します。

MS\_SMHBA\_PROTOCOLSTATISTICS クラスは、 *Hbaapi .mof*で次のように定義されています。

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

このクラス定義が WMI ツールスイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SMHBA\_PROTOCOLSTATISTICS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_protocolstatistics)

この WMI クラスに関連付けられているメソッドはありません。

 

 





