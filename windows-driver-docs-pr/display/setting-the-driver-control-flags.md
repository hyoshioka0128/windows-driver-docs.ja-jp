---
title: ドライバー制御フラグの設定
description: ドライバー制御フラグの設定
ms.assetid: cca51b9c-ce37-4efb-ab42-8eb62b25eb21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a10fd71af917dd6e946328afc319e60ae7c3e22
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390437"
---
# <a name="setting-the-driver-control-flags"></a>ドライバー制御フラグの設定


**ExcludeFromSelect**以外のすべてのドライバーのディレクティブが必要な[ミラー ドライバー](mirror-drivers.md)、Windows Display Driver Model (WDDM) に書き込まれます。

次の例は、追加する方法を示します、 **ExcludeFromSelect**ディレクティブを**ControlFlags** INF ファイルのセクション。

```inf
[ControlFlags]
ExcludeFromSelect=*
```

ドライバーの制御フラグの詳細については、次を参照してください。 [ **INF ControlFlags セクション**](https://msdn.microsoft.com/library/windows/hardware/ff546342)します。

 

 





