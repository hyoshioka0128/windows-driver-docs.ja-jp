---
title: 現在の接続のオフロード設定を決定します。
description: 現在の接続のオフロード設定を決定します。
ms.assetid: aca377ae-c56b-4f84-8165-4b084bfa9938
keywords:
- 接続の負荷を軽減 WDK TCP/IP トランスポートでは、現在の設定
- 現在の接続の負荷を軽減 WDK TCP/IP offload の設定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 530cf5aeebbd3462c2ba51eb761618e5471f6a06
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558350"
---
# <a name="determining-the-current-connection-offload-settings"></a>現在の接続のオフロード設定を決定します。





プロトコル ドライバーでは、オブジェクト識別子 (OID) 要求にオフロード サービス接続を取得できます。

ネットワーク インターフェイス カード (NIC) のオフロード設定を現在の接続を取得するプロトコル ドライバーがクエリできる、 [OID\_TCP\_接続\_オフロード\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569804) OID。

 

 





