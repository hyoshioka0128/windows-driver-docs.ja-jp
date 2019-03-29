---
title: MPIO\_コント ローラー\_情報 WMI クラス
description: MPIO\_コント ローラー\_情報 WMI クラス
ms.assetid: 0448e056-2bbe-4e4f-a729-a872393222e5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 81e51f737eb560c3ba18a27f7faf070468961792
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574633"
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

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **MPIO\_コント ローラー\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff562329)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





