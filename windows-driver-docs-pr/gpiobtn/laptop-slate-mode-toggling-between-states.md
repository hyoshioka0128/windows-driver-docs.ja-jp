---
title: ラップトップ/スレート モードの状態の切り替え
description: このトピックでには、ラップトップ/スレート モードのインジケーターの状態を切り替えるためのサンプル コードが含まれています。
ms.assetid: C5D9B586-EED7-4DC7-8BFF-3AB3A972307D
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e35e21cb956921d870384b8aa76a08a201b518ad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529813"
---
# <a name="laptopslate-mode-toggling-between-states"></a>ラップトップ/スレート モードの状態の切り替え


このトピックでには、ラップトップ/スレート モードのインジケーターの状態を切り替えるためのサンプル コードが含まれています。

```cpp
int __cdecl ToggleConversionIndicator(
    __in int argc,
    __in_ecount(argc) char **argv)
{
    LPWSTR DevicePath;
    HANDLE FileHandle;
    BOOL b;
    BYTE buffer;
    HWND hwnd;
    MSG msg;

//assuming our GetDevicePath method is creating a device path using use SetupDi API
    DevicePath = GetDevicePath((LPGUID)&amp;GUID_GPIOBUTTONS_LAPTOPSLATE_INTERFACE);
   
    FileHandle = CreateFile(DevicePath,
                            GENERIC_WRITE,
                            0,
                            NULL,
                            OPEN_EXISTING,
                            0,
                            NULL);
   
    buffer = 0;
    WriteFile(FileHandle, &amp;buffer, sizeof(buffer), NULL, NULL);

    return 0;
}
```

 

 




