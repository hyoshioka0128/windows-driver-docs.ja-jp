---
title: MPIO\_ドライブ\_情報 WMI クラス
description: MPIO\_ドライブ\_情報 WMI クラス
ms.assetid: 4c116157-5f5b-4213-abdd-9128ebbfa341
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7a1e4a6d443c172f88f49c7947e7bd1b920b2177
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391406"
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
    // The real device's serial number.
    //
    [WmiDataId(3), MaxLen(63)] string SerialNumber;

    //
    // Friendly name of the DSM controlling the device.
    //
    [WmiDataId(4), MaxLen(63)] string DsmName;
};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **MPIO\_ドライブ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff562377)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





