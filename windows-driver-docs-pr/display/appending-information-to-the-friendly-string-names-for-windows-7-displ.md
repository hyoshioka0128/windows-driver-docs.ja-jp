---
title: Windows 7 のディスプレイ ドライバーのフレンドリ名に情報を追加します。
description: Windows 7 のディスプレイ ドライバーの名前をわかりやすい文字列に追加する必要があります情報について説明します。
ms.assetid: 8c65f3d9-6f4c-49e9-a9b2-2689d83a181c
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 3541b8030ca6be161a7275aaf63bcd078387d0d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553700"
---
# <a name="appending-information-to-the-friendly-string-names-for-windows-7-display-drivers"></a>Windows 7 のディスプレイ ドライバーのわかりやすい文字列名に情報を追加


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

グラフィックス アダプターのフレンドリ名は、すべて Windows 7 のボックスでのディスプレイ ドライバーの INF で必要なローカライズ可能な文字列名です。 に関するセクション[フレンドリ文字列名のグラフィックス アダプターを追加することについて](appending-information-to-the-friendly-string-names-of-graphics-adapter.md)を追加する必要があります Windows Display Driver Model (WDDM) の情報について説明しますと、 [Windows 2000 のディスプレイ ドライバーモデル](windows-2000-display-driver-model-design-guide.md)します。 Windows 7 用に最適化された、WDDM の"(Microsoft Corporation の WDDM v1.1)"を追加する必要があります。

```cpp
New Driver Model Foo Device Name (Microsoft Corporation - WDDM v1.1)
```

グラフィックス アダプターのフレンドリ名に追加するテキストには、ドライバーを使用する WDDM バージョンを指定します。

 

 





