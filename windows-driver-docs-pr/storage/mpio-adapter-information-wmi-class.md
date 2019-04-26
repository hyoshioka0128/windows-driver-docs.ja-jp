---
title: MPIO\_アダプター\_情報 WMI クラス
description: MPIO\_アダプター\_情報 WMI クラス
ms.assetid: 748205a5-d37b-4080-b6ce-9176139cef4a
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8616dd4021da05b66fee64b940a6a3e9f93716ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339593"
---
# <a name="mpioadapterinformation-wmi-class"></a>MPIO\_アダプター\_情報 WMI クラス


MPIO ドライバーは、MPIO を使用して\_アダプター\_MPIO ディスクに関連付けられているパスを識別する情報の WMI クラスです。

```cpp
class MPIO_ADAPTER_INFORMATION
{
    //
    // Path ID. The PDO_INFORMATION class includes
    // it's pathId. These values can be used to find
    // which devices are on which path.
    //
    [WmiDataId(1)] uint64 PathId;

    //
    // Adapter Location.
    //
    [WmiDataId(2)] uint8 BusNumber;
    [WmiDataId(3)] uint8 DeviceNumber;
    [WmiDataId(4)] uint8 FunctionNumber;
    [WmiDataId(5)] uint8 Pad;

    //
    // Adapter Name.
    //
    [WmiDataId(6), MaxLen(63)] string AdapterName;
};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **MPIO\_アダプター\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff562313)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





