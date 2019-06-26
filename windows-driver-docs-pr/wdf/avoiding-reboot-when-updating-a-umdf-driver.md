---
title: UMDF ドライバー更新時の再起動の回避
description: UMDF ドライバー更新時の再起動の回避
ms.assetid: B5321732-50FD-4719-BBD0-F0A3BE1EE532
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d26ee878d1f74cedd88ce6c48d9e76b0fb45632
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379040"
---
# <a name="avoiding-reboot-when-updating-a-umdf-driver"></a>UMDF ドライバー更新時の再起動の回避


必要な再起動を避けるためには、UMDF ドライバーを更新するときに、指定、 **COPYFLG\_IN\_使用\_の名前を変更**フラグ、 [ **CopyFiles ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)でこの例で示すように、ドライバーの INF ファイル。

```cpp
[VirtualSerial_Install.NT]
CopyFiles=UMDriverCopy
 
[UMDriverCopy]
Virtualserial.dll,,,0x00004000  ; COPYFLG_IN_USE_RENAME
```

 

 





