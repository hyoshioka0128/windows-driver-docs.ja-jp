---
title: Winsock カーネル拡張インターフェイス
description: Winsock カーネル拡張インターフェイス
ms.assetid: db0030fa-0ee9-482b-b6ba-e95b40a25473
keywords:
- Winsock カーネル WDK がネットワーク接続、拡張機能インターフェイス
- WSK WDK のネットワーク接続、拡張機能インターフェイス
- 拡張機能インターフェイス WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22d75375e7bd45b526d71ac201af3c02e1cc18df
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360212"
---
# <a name="winsock-kernel-extension-interfaces"></a>Winsock カーネル拡張インターフェイス


Winsock カーネル (WSK)[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md)のサポートが含まれています*拡張機能インターフェイス*します。 WSK サブシステムは、拡張機能インターフェイスを使用して、WSK sockets ソケットの関数と WSK NPI で現在定義されているイベントのコールバック関数の一連の機能を拡張することができます。 各拡張機能インターフェイスは、WSK NPI から独立している、NPI によって定義されます。 現在の拡張機能インターフェイスが定義されていません。

使用して、WSK サブシステムでサポートされている拡張機能インターフェイスの WSK アプリケーションを登録できます、 [ **SIO\_WSK\_登録\_拡張子**](https://docs.microsoft.com/windows-hardware/drivers/network/sio-wsk-register-extension)ソケットIOCTL 操作です。 ソケットのソケットによってごとに拡張機能インターフェイス WSK アプリケーションを登録します。

拡張機能インターフェイスを登録の詳細については、次を参照してください。[拡張機能インターフェイスを登録する](registering-an-extension-interface.md)します。

 

 





