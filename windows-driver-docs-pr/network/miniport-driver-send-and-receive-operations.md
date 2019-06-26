---
title: ミニポート ドライバーの送信および受信操作
description: ミニポート ドライバーの送信および受信操作
ms.assetid: f495cf1f-9896-4259-b885-cff4a0112d17
keywords:
- ミニポート ドライバー WDK ネットワークは、データを送信します。
- NDIS ミニポート ドライバー WDK、データを送信します。
- ミニポート ドライバー WDK ネットワークは、データの受信
- NDIS ミニポート ドライバー WDK、データの受信
- WDK ネットワークのデータを送信します。
- 受信側のデータの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abbc1ae089524f5aad0b25872bbcff60e1667a31
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373934"
---
# <a name="miniport-driver-send-and-receive-operations"></a>ミニポート ドライバーの送信および受信操作





ハンドルが重なってドライバーから要求を送信および発信のミニポート ドライバーでは、インジケーターが表示されます。 1 つの関数の呼び出しで NDIS ミニポート ドライバーは、受信した複数のリンクされたリストを指定できます[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。 ミニポート ドライバーが複数のネットワークの一覧については、送信要求を処理できる\_バッファー\_複数のリストの構造体[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)各ネットワーク上の構造\_バッファー\_リスト構造体。

ミニポート ドライバーを管理する必要があるバッファー プールを受信します。 ほとんどのミニポート ドライバーが事前に割り当てる 1 つの NET するプールを作成\_各 NET でバッファー構造\_バッファー\_リスト構造体。

次のトピックは、ミニポート ドライバー バッファー管理の詳細について説明し、操作を送信、受信操作。

[ミニポート ドライバー バッファー管理](miniport-driver-buffer-management.md)

[ミニポート ドライバーからデータを送信します。](sending-data-from-a-miniport-driver.md)

[ミニポート ドライバーでは、送信要求を取り消す](canceling-a-send-request-in-a-miniport-driver.md)

[ミニポート ドライバーからデータを受信したことを示します](indicating-received-data-from-a-miniport-driver.md)

 

 





