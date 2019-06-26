---
title: MPIO\_コント ローラー\_情報 WMI クラス
description: MPIO\_コント ローラー\_情報 WMI クラス
ms.assetid: 0448e056-2bbe-4e4f-a729-a872393222e5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 61f3df09cb9d28a4f13a6e99cd8709c2090203d3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386174"
---
# <a name="mpiocontrollerinfo-wmi-class"></a>MPIO\_コント ローラー\_情報 WMI クラス


MPIO ドライバーは、MPIO を使用して\_コント ローラー\_記憶域コント ローラーとその関連付けられている DSM を識別する情報の WMI クラスです。

```cpp
class MPIO_CONTROLLER_INFO
{

    //
    // Devices behind this controller will have a matching
    // ControllerId in the PDO_INFORMATION class.
    //
    [WmiDataId(1)] uint32 IdentifierType;
    [WmiDataId(2)] uint32 IdentifierLength;
    [WmiDataId(3)] uint8 Identifier[32];
    [WmiDataId(4)] uint32 ControllerState;
    [WmiDataId(5)] uint32 Pad;
    [WmiDataId(6), MaxLen(63)] string AssociatedDsm;
};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **MPIO\_コント ローラー\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiowmi/ns-mpiowmi-_mpio_controller_info)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





