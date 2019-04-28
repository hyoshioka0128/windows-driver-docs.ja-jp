---
title: 現在の接続オフロード設定の判断
description: 現在の接続オフロード設定の判断
ms.assetid: aca377ae-c56b-4f84-8165-4b084bfa9938
keywords:
- 接続の負荷を軽減 WDK TCP/IP トランスポートでは、現在の設定
- 現在の接続の負荷を軽減 WDK TCP/IP offload の設定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 530cf5aeebbd3462c2ba51eb761618e5471f6a06
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364188"
---
# <a name="determining-the-current-connection-offload-settings"></a>現在の接続オフロード設定の判断





プロトコル ドライバーでは、オブジェクト識別子 (OID) 要求にオフロード サービス接続を取得できます。

ネットワーク インターフェイス カード (NIC) のオフロード設定を現在の接続を取得するプロトコル ドライバーがクエリできる、 [OID\_TCP\_接続\_オフロード\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569804) OID。

 

 





