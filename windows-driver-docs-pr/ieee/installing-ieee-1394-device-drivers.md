---
title: IEEE 1394 デバイス ドライバーのインストール
description: IEEE 1394 デバイス ドライバーのインストール
ms.assetid: 3f99bec7-e657-4de7-bce4-36a779cc0442
keywords:
- IEEE 1394 WDK バス ドライバーのインストール
- 1394 WDK バス ドライバーのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8f1a4454b102f00aa4187aa475564c39b0ffdd2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371056"
---
# <a name="installing-ieee-1394-device-drivers"></a>IEEE 1394 デバイス ドライバーのインストール





このセクションでは、インストールについては、Microsoft Windows 2000 以降のオペレーティング システムでの IEEE 1394 デバイス ドライバーに固有では。

独自の IEEE 1394 デバイス ドライバーを提供しているベンダー ドライバーを行う必要がありますで基本セットアップ クラスのメンバー、 [ **INF バージョン セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547502)ドライバーの INF ファイル。 次に、例を示します。

```cpp
[Version]
Signature="$WINDOWS NT$"
Class = Base
```

IEEE 1394 デバイス ドライバーのインストールに関連付けられているその他の特別な要件はありません。

Windows 2000 以降のオペレーティング システムでデバイスのインストールの詳細については、次を参照してください。[デバイス インストールの概要](https://msdn.microsoft.com/library/windows/hardware/ff549455)します。

 

 




