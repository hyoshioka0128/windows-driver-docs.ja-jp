---
title: プロトコル ドライバーの送信および受信操作
description: プロトコル ドライバーの送信および受信操作
ms.assetid: c621d673-167e-41e1-a121-68e0d0bc6f8a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 543cd0e1e96f693d3bcf9b3b16a5da28bf5fcc78
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385459"
---
# <a name="protocol-driver-send-and-receive-operations"></a>プロトコル ドライバーの送信および受信操作





プロトコル ドライバーでは、送信要求を発信し、基になるドライバーの受信の兆候を処理します。 1 つの関数呼び出しでは、NDIS プロトコル ドライバーが複数送信できます[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)複数構造[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造で各 NET\_バッファー\_リスト構造体。 プロトコル ドライバー受信パスでは、NET の一覧を受信できる\_バッファー\_リストの構造体。

プロトコル ドライバーには、送信するバッファー プールを管理する必要があります。 このようなプールの適切な管理には、システムのパフォーマンスを最適化するために十分なバッファー領域の事前割り当てが必要です。

次のトピックは、プロトコル ドライバー バッファー管理の詳細について説明し、操作を送信、受信操作。

[プロトコル ドライバー バッファー管理](protocol-driver-buffer-management.md)

[プロトコル ドライバーからデータを送信します。](sending-data-from-a-protocol-driver.md)

[プロトコル ドライバーにデータの受信](receiving-data-in-protocol-drivers.md)

 

 





