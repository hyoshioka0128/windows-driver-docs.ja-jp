---
title: 受信パスでの IPsec タスクのオフロード
description: 受信パスでの IPsec タスクのオフロード
ms.assetid: d1dff4fa-7354-4c8c-8591-223c6b524619
keywords:
- ESP で保護されたパケットの WDK IPsec オフロード、受信パスオフロード
- AH で保護されたパケット WDK IPsec オフロード、受信パスオフロード
- 受信パスオフロード WDK IPsec オフロード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24bcb84fbd67fdf61f255fb8dbde9c5d220d4065
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834633"
---
# <a name="offloading-ipsec-tasks-in-the-receive-path"></a>受信パスでの IPsec タスクのオフロード

\[IPsec タスクオフロード機能は非推奨とされているため、使用しないでください。\]




NIC は、受信パケットでインターネットプロトコルセキュリティ (IPsec) 処理を実行します。パケットに ESP ペイロードが含まれている場合は、パケットの暗号化を解除し、パケットに対して AH または ESP の暗号化チェックサム (またはその両方) を計算します。 パケットに関連付けられているパケットの[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造を指定する前に、ポートの\_*Id*が**IPsecOffloadV1NetBufferListInfo**の[**net\_buffer\_list\_info**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)マクロを呼び出して、 [**NDIS\_IPSEC\_オフロード\_V1\_NET\_BUFFER\_LIST\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v1_net_buffer_list_info)構造体を取得します。

ミニポートドライバーは、NDIS\_IPSEC\_オフロード\_V1\_NET\_BUFFER\_LIST\_INFO 構造体の**Cryptodone**フラグを設定して、NIC が少なくとも1つの ipsec ペイロードに対して ipsec チェックを実行したことを示します。受信パケット内。 NIC が受信パケットのトンネルとトランスポートの両方の部分に対して IPsec チェックを実行した場合、ミニポートドライバーは、NDIS\_IPSEC\_OFFLOAD\_V1\_NET\_BUFFER\_LIST にある**Nextcryptodone**フラグも設定します。\_情報構造体。 ミニポートドライバーは、パケットにトンネルとトランスポートの両方の IPsec ペイロードがある場合にのみ、 **Nextcryptodone**を設定します。 それ以外の場合、ミニポートドライバーは**Nextcryptodone**を0に設定します。 IPsec チェックの結果を示すために、ミニポートドライバーは、NDIS\_IPSEC\_オフロード\_V1\_NET\_BUFFER\_LIST\_INFO 構造体の**Cryptostatus**メンバーの値も指定する必要があります。 NIC がチェックサムの失敗または復号化の失敗を検出した場合、ミニポートドライバーは、受信パケットの[ **\_リスト構造\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)を任意の形式で示し、適切な**cryptostatus**値を指定する必要があります。

ミニポートドライバーが受信パケットを復号化していない場合は、 **cryptodone**フラグと**nextcryptodone**フラグの両方がクリアされます。 ミニポートドライバーは、パケットが AH で保護されているか、または ESP で保護されているかに関係なく、暗号化を解除しないすべての受信パケットに対してこれを行います。 ミニポートドライバーは、暗号化を解除しないすべてのパケットに対して、 **Cryptostatus**を CRYPTO\_に設定します。

ミニポートドライバーによって、ネットワーク\_バッファー\_一覧構造が TCP/IP トランスポートに示された後、トランスポートは、NIC が実行した IPsec チェックの結果を調べ、パケットのシーケンス番号を確認して、チェックサムテストまたはシーケンステストに失敗したパケット。

 

 





