---
title: IEEE 1394 デバイス ドライバーのインストール
description: IEEE 1394 デバイス ドライバーのインストール
ms.assetid: 3f99bec7-e657-4de7-bce4-36a779cc0442
keywords:
- IEEE 1394 WDK バス ドライバーのインストール
- 1394 WDK バス ドライバーのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37bdefa6af9a51303dd10f8c9ea930cce95e0022
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385767"
---
# <a name="installing-ieee-1394-device-drivers"></a>IEEE 1394 デバイス ドライバーのインストール





このセクションでは、インストールについては、Microsoft Windows 2000 以降のオペレーティング システムでの IEEE 1394 デバイス ドライバーに固有では。

独自の IEEE 1394 デバイス ドライバーを提供しているベンダー ドライバーを行う必要がありますで基本セットアップ クラスのメンバー、 [ **INF バージョン セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)ドライバーの INF ファイル。 次に、例を示します。

```cpp
[Version]
Signature="$WINDOWS NT$"
Class = Base
```

IEEE 1394 デバイス ドライバーのインストールに関連付けられているその他の特別な要件はありません。

Windows 2000 以降のオペレーティング システムでデバイスのインストールの詳細については、次を参照してください。[デバイス インストールの概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-and-driver-installation)します。

 

 




