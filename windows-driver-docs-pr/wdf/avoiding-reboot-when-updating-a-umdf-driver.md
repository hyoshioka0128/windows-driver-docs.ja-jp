---
title: UMDF ドライバー更新時の再起動の回避
description: UMDF ドライバー更新時の再起動の回避
ms.assetid: B5321732-50FD-4719-BBD0-F0A3BE1EE532
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e4edba5e0044bee795a5c3b65544cfb34806f89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331195"
---
# <a name="avoiding-reboot-when-updating-a-umdf-driver"></a>UMDF ドライバー更新時の再起動の回避


必要な再起動を避けるためには、UMDF ドライバーを更新するときに、指定、 **COPYFLG\_IN\_使用\_の名前を変更**フラグ、 [ **CopyFiles ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546346)でこの例で示すように、ドライバーの INF ファイル。

```cpp
[VirtualSerial_Install.NT]
CopyFiles=UMDriverCopy
 
[UMDriverCopy]
Virtualserial.dll,,,0x00004000  ; COPYFLG_IN_USE_RENAME
```

 

 





