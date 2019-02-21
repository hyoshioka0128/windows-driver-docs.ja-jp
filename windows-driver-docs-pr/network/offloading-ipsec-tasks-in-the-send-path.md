---
title: 送信パスで IPsec タスクをオフロード
description: 送信パスで IPsec タスクをオフロード
ms.assetid: b95878e0-0aee-43cb-a64c-b5d8e07cb1b4
keywords:
- WDK IPsec オフロード、ESP により保護されたパケットの送信パスのオフロード
- WDK IPsec オフロード、AH で保護されたパケットの送信パスのオフロード
- パスのオフロード WDK IPsec オフロードを送信します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ced113f09c7b91db094da2e954446eb31753e777
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553773"
---
# <a name="offloading-ipsec-tasks-in-the-send-path"></a>送信パスで IPsec タスクをオフロード

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




TCP/IP トランスポートは、ミニポート ドライバーに渡される前に、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388) NIC がインターネット プロトコル セキュリティ (IPsec) を実行するパケットの構造ネットワークに関連付けられている IPsec 情報更新タスク、\_バッファー\_リスト構造体。 TCP/IP トランスポートでは、この情報を指定します、 [ **NDIS\_IPSEC\_オフロード\_V1\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565801)構造体は、ネットワークの一部である\_バッファー\_リストの情報 (帯域外のデータ)、NET に関連付けられている\_バッファー\_リスト構造体。

TCP/IP トランスポートを提供*OffloadHandle*トランスポート (エンド ツー エンド接続) 部分の送信パケットの送信、SA を識別するハンドルを指定します。 パケットは、トンネル経由送信は、指定すると、TCP/IP トランスポートも提供*NextOffloadHandle*、送信パケットの部分のトンネルの送信、SA を識別するハンドルを指定します。

ドライバーの受信後、ミニポート、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体の[ *MiniportSendNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff559440)または[ **MiniportCoSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff559365)関数を呼び出すことが、 [ **NET\_バッファー\_]ボックスの一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff568401)マクロが、  *\_Id*の**IPsecOffloadV1NetBufferListInfo** NDIS を取得する\_IPSEC\_オフロード\_V1\_NET\_バッファー\_一覧\_NET に関連付けられている情報の構造体\_バッファー\_リスト構造体。

NIC は、IPsec の送信パケットの処理を実行するときに、パケットの (またはその両方) を AH または ESP 暗号化チェックサムを計算し、パケットには、ESP ペイロードが含まれている場合は、パケットを暗号化します。 TCP/IP トランスポートが既にパケットをフレーム化、し (必要に応じて) が埋め込まれておよびシーケンス番号および SPI 割り当てられています。

 

 





