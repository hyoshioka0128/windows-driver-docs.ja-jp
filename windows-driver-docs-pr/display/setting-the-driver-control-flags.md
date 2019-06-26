---
title: ドライバー制御フラグの設定
description: ドライバー制御フラグの設定
ms.assetid: cca51b9c-ce37-4efb-ab42-8eb62b25eb21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6465e13c11f5f75b2b0fb1cb5fce098849e510b6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365559"
---
# <a name="setting-the-driver-control-flags"></a>ドライバー制御フラグの設定


**ExcludeFromSelect**以外のすべてのドライバーのディレクティブが必要な[ミラー ドライバー](mirror-drivers.md)、Windows Display Driver Model (WDDM) に書き込まれます。

次の例は、追加する方法を示します、 **ExcludeFromSelect**ディレクティブを**ControlFlags** INF ファイルのセクション。

```inf
[ControlFlags]
ExcludeFromSelect=*
```

ドライバーの制御フラグの詳細については、次を参照してください。 [ **INF ControlFlags セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-controlflags-section)します。

 

 





