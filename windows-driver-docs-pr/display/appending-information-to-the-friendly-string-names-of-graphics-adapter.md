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
ms.openlocfilehash: a2828317136a7c3be2b23310a2b28f59778f7b2d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385034"
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

詳細については、*文字列*セクションおよび *%strkey* 、INF で他の場所で指定されているトークンを参照してください[ **INF 文字列セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547485).

 

 





