---
title: プロトコル ドライバーの送信および受信操作
description: プロトコル ドライバーの送信および受信操作
ms.assetid: c621d673-167e-41e1-a121-68e0d0bc6f8a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8b8ca1752ad284f47cf3bffd625eefe26211398
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844907"
---
# <a name="protocol-driver-send-and-receive-operations"></a>プロトコル ドライバーの送信および受信操作





プロトコルドライバーは、送信要求を発信し、基になるドライバーの受信表示を処理します。 1回の関数呼び出しでは、NDIS プロトコルドライバーは、各 NET\_BUFFER\_LIST 構造体に複数の[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造を持つ複数の[**net\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造を送信できます。 受信パスでは、プロトコルドライバーは、NET\_BUFFER\_LIST 構造体の一覧を受け取ることができます。

プロトコルドライバーは、送信バッファープールを管理する必要があります。 これらのプールを適切に管理するには、システムパフォーマンスを最適化するために十分なバッファー領域を事前に割り当てておく必要があります。

次のトピックでは、プロトコルドライバーのバッファー管理、送信操作、および受信操作の詳細について説明します。

[プロトコルドライバーのバッファー管理](protocol-driver-buffer-management.md)

[プロトコルドライバーからのデータの送信](sending-data-from-a-protocol-driver.md)

[プロトコルドライバーでのデータの受信](receiving-data-in-protocol-drivers.md)

 

 





