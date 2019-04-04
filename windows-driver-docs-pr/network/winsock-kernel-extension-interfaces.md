---
title: Winsock カーネルの拡張機能インターフェイス
description: Winsock カーネルの拡張機能インターフェイス
ms.assetid: db0030fa-0ee9-482b-b6ba-e95b40a25473
keywords:
- Winsock カーネル WDK がネットワーク接続、拡張機能インターフェイス
- WSK WDK のネットワーク接続、拡張機能インターフェイス
- 拡張機能インターフェイス WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45126db08fc387f48b798fceead8807cf28d1f60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530143"
---
# <a name="winsock-kernel-extension-interfaces"></a>Winsock カーネルの拡張機能インターフェイス


Winsock カーネル (WSK)[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md)のサポートが含まれています*拡張機能インターフェイス*します。 WSK サブシステムは、拡張機能インターフェイスを使用して、WSK sockets ソケットの関数と WSK NPI で現在定義されているイベントのコールバック関数の一連の機能を拡張することができます。 各拡張機能インターフェイスは、WSK NPI から独立している、NPI によって定義されます。 現在の拡張機能インターフェイスが定義されていません。

使用して、WSK サブシステムでサポートされている拡張機能インターフェイスの WSK アプリケーションを登録できます、 [ **SIO\_WSK\_登録\_拡張子**](https://msdn.microsoft.com/library/windows/hardware/ff570819)ソケットIOCTL 操作です。 ソケットのソケットによってごとに拡張機能インターフェイス WSK アプリケーションを登録します。

拡張機能インターフェイスを登録の詳細については、[拡張機能インターフェイスを登録する](registering-an-extension-interface.md)を参照してください。

 

 





