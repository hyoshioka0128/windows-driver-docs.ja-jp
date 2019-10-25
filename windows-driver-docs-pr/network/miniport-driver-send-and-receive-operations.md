---
title: ミニポート ドライバーの送信および受信操作
description: ミニポート ドライバーの送信および受信操作
ms.assetid: f495cf1f-9896-4259-b885-cff4a0112d17
keywords:
- ミニポートドライバー WDK ネットワーク、送信 (データを)
- NDIS ミニポートドライバー WDK、データの送信
- ミニポートドライバー WDK ネットワーク、受信データ
- NDIS ミニポートドライバー WDK、データの受信
- データの送信 (WDK ネットワーク)
- データを受信する WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db3e70c1201ab6e293b1b473b6e15caa91ec9313
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844238"
---
# <a name="miniport-driver-send-and-receive-operations"></a>ミニポート ドライバーの送信および受信操作





ミニポートドライバーは、それ以降のドライバーからの送信要求を処理し、受信通知を発信します。 1回の関数呼び出しで、NDIS ミニポートドライバーは、複数の受信した[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造を持つリンクリストを示すことができます。 ミニポートドライバーは、各 NET\_BUFFER\_LIST 構造体に複数の[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造を持つ複数の NET\_BUFFER\_リスト構造のリストに対する送信要求を処理できます。

ミニポートドライバーは、受信バッファープールを管理する必要があります。 ほとんどのミニポートドライバーは、各 NET\_BUFFER\_LIST 構造体を使用して、1つの NET\_バッファー構造を事前に割り当てるプールを作成します。

次のトピックでは、ミニポートドライバーのバッファー管理、送信操作、および受信操作の詳細について説明します。

[ミニポートドライバーのバッファー管理](miniport-driver-buffer-management.md)

[ミニポートドライバーからのデータの送信](sending-data-from-a-miniport-driver.md)

[ミニポートドライバーで送信要求をキャンセルする](canceling-a-send-request-in-a-miniport-driver.md)

[ミニポートドライバーからの受信データを示す](indicating-received-data-from-a-miniport-driver.md)

 

 





