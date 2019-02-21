---
title: ドライバーの制御フラグを設定
description: ドライバーの制御フラグを設定
ms.assetid: cca51b9c-ce37-4efb-ab42-8eb62b25eb21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a10fd71af917dd6e946328afc319e60ae7c3e22
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530412"
---
# <a name="setting-the-driver-control-flags"></a>ドライバーの制御フラグを設定


**ExcludeFromSelect**以外のすべてのドライバーのディレクティブが必要な[ミラー ドライバー](mirror-drivers.md)、Windows Display Driver Model (WDDM) に書き込まれます。

次の例は、追加する方法を示します、 **ExcludeFromSelect**ディレクティブを**ControlFlags** INF ファイルのセクション。

```inf
[ControlFlags]
ExcludeFromSelect=*
```

ドライバーの制御フラグの詳細については、次を参照してください。 [ **INF ControlFlags セクション**](https://msdn.microsoft.com/library/windows/hardware/ff546342)します。

 

 





