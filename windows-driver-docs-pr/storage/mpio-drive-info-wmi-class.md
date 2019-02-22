---
title: MPIO\_ドライブ\_情報 WMI クラス
description: MPIO\_ドライブ\_情報 WMI クラス
ms.assetid: 4c116157-5f5b-4213-abdd-9128ebbfa341
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 91f2d7833888e8c0ab3178be944ac05160ec807c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527306"
---
# <a name="mpiodriveinfo-wmi-class"></a>MPIO\_ドライブ\_情報 WMI クラス


MPIO ドライバーは、MPIO を使用して\_ドライブ\_管理しているシステム上の各 MPIO ディスクを識別する情報の WMI クラスです。

```cpp
class MPIO_DRIVE_INFO
{
    //
    // Number of Paths to the real device.
    //
    [WmiDataId(1)] uint32 NumberPaths;

    //
    // The MPIODisk(N).
    //
    [WmiDataId(2), MaxLen(63)] string Name;

    //
    // The real device&#39;s serial number.
    //
    [WmiDataId(3), MaxLen(63)] string SerialNumber;

    //
    // Friendly name of the DSM controlling the device.
    //
    [WmiDataId(4), MaxLen(63)] string DsmName;
};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **MPIO\_ドライブ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff562377)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





