---
title: 現在の接続オフロード設定の判断
description: 現在の接続オフロード設定の判断
ms.assetid: aca377ae-c56b-4f84-8165-4b084bfa9938
keywords:
- 接続の負荷を軽減 WDK TCP/IP トランスポートでは、現在の設定
- 現在の接続の負荷を軽減 WDK TCP/IP offload の設定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2b11a46fa7702715d332ded4994644ac21770f7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353354"
---
# <a name="determining-the-current-connection-offload-settings"></a>現在の接続オフロード設定の判断





プロトコル ドライバーでは、オブジェクト識別子 (OID) 要求にオフロード サービス接続を取得できます。

ネットワーク インターフェイス カード (NIC) のオフロード設定を現在の接続を取得するプロトコル ドライバーがクエリできる、 [OID\_TCP\_接続\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-parameters) OID。

 

 





