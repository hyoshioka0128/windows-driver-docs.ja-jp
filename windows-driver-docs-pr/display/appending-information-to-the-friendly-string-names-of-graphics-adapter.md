---
title: グラフィックス アダプターのフレンドリ文字列名に情報を追加する
description: グラフィックス アダプターの文字列名には、情報を追加する必要があります。
ms.assetid: 660104ba-b082-407b-afdc-3e02f4c3d087
keywords:
- INF ファイル WDK の表示、わかりやすい文字列名
- わかりやすい文字列名 WDK の表示
- グラフィックス アダプターは、WDK の表示名を文字列します。
- グラフィックス アダプターに WDK を表示する文字列名を追加します。
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: c683f9e92d8140cf3630c880965ee18da38a0b0d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384641"
---
# <a name="appending-information-to-the-friendly-string-names-of-graphics-adapters"></a>グラフィックス アダプターのわかりやすい文字列名に情報を追加


グラフィックス アダプターの文字列名には、情報を追加する必要があります。 この情報は、アダプターのドライバーに書き込まれたディスプレイ ドライバー モデルによって異なります。

Windows 2000 Display Driver Model の"(Microsoft Corporation) を追加する必要があります"。

```cpp
XDDM Foo Device Name (Microsoft Corporation)
```

Windows Display Driver Model (WDDM) の"(Microsoft Corporation の WDDM)"を追加する必要があります。

```cpp
New Driver Model Foo Device Name (Microsoft Corporation - WDDM)
```

詳細については、*文字列*セクションおよび *%strkey* 、INF で他の場所で指定されているトークンを参照してください[ **INF 文字列セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section).

 

 





