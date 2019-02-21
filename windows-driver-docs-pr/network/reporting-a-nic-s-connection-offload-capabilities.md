---
title: NIC の接続のオフロード機能の報告
description: NIC の接続のオフロード機能の報告
ms.assetid: a9bf798b-382c-4904-b0b2-ed1e54f9c36b
keywords:
- 接続は、WDK TCP/IP トランスポートは、レポート機能をオフロードします。
- レポート接続のオフロード機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1608e2c07905df3d4fefcc6de2aa479ec636857c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560623"
---
# <a name="reporting-a-nics-connection-offload-capabilities"></a>NIC の接続のオフロード機能の報告





NDIS ミニポート ドライバーでは、NIC の現在の接続オフロードの構成を指定します、 [ **NDIS\_TCP\_接続\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff567875)構造体。 ミニポート ドライバーでの現在の接続オフロードの構成を含める必要があります、 [ **NDIS\_ミニポート\_アダプター\_オフロード\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565930)構造体。 ミニポート ドライバーの呼び出し、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数を[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数を渡す、NDIS 情報\_ミニポート\_TCP\_接続\_オフロード\_属性。

ミニポート ドライバーでは、オフロード機能を接続の変更を報告する必要があります。 ドライバーは、スタックを一時停止し、状態を示す値を発行してアップロードするすべての接続を要求します。 (NDIS について\_状態\_オフロード\_一時停止を参照してください[完全な TCP オフロード](full-tcp-offload.md))。構成の変更が完了した後、ドライバーを再起動し、状態を示す値を発行してミニポート アダプターのオフロード機能を再クエリ スタックを要求します。 (NDIS について\_状態\_オフロード\_再開、完全な TCP オフロードを参照してください)。

クエリに対する応答で[OID\_TCP\_接続\_オフロード\_現在\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569802)、NDIS を返します、 [ **NDIS\_TCP\_接続\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff567875)構造体、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体。 NDIS は、ミニポート ドライバーが提供される情報を使用します。

オフロード機能の接続の指定の詳細についてでのオフロードのターゲットの初期化を参照してください、 [NDIS 6.0 TCP chimney オフロード ドキュメント](full-tcp-offload.md)します。

 

 





