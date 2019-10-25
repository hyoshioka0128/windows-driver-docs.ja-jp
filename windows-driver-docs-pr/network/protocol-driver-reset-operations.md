---
title: プロトコル ドライバー リセット操作
description: プロトコル ドライバー リセット操作
ms.assetid: 862029e5-8c46-4889-80f5-15c463f228a3
keywords:
- プロトコルドライバー WDK ネットワーク、リセット操作
- NDIS プロトコルドライバーの WDK、リセット操作
- リセット操作 WDK NDIS プロトコル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b15478f92db5763ec55ce910bc49fd16631ad5a2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844909"
---
# <a name="protocol-driver-reset-operations"></a>プロトコル ドライバー リセット操作





プロトコルドライバーは、NDIS 6.0 以降のバージョンでリセット操作を開始することはできません。

通常、送信または要求の操作中に NIC がタイムアウトになるため、基になるミニポートドライバーによって NIC がリセットされます。 この条件により、NDIS はミニポートドライバーの[*MiniportCheckForHangEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_check_for_hang)を呼び出し、その後に[*Miniportresetex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)関数を呼び出します。 また、ミニポートドライバーは、NIC の受信機能が不充足であると判断します。

NDIS によってリセットが開始され、 *Miniportresetex*が NDIS\_STATUS\_PENDING を返した場合、NDIS は ndis の状態を使用して、バインドされた各プロトコルドライバーの[**protocolstatusex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex)(または[**protocolcostatusex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_status_ex)) 関数を呼び出し\_状態\_リセット\_開始します。 ミニポートドライバーが[**NdisMResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismresetcomplete)を呼び出すと、Ndis は*protocolstatusex*(または*protocolcostatusex*) を再度呼び出します。状態は NDIS\_status\_リセット\_終了です。

プロトコルドライバーは、NIC がリセットされるため、基になる NIC へのバインドに対する未処理の送信がキャンセルされる可能性を処理する必要があります。 バインドされたプロトコルドライバーに送信要求が保留中の場合、NDIS は適切な状態でプロトコルドライバーへの送信が完了したことを示します。 リセット操作が完了すると、プロトコルドライバーは送信要求を再送信する必要があります。 NIC が再び操作可能になると想定されます。

プロトコルドライバが NDIS\_STATUS の状態を受信し\_リセット\_開始したら、次のことを行う必要があります。

-   *プロトコル (Co) の状態*が NDIS\_状態になるまで、送信可能なすべてのネットワークデータを保持し、\_エンド通知\_リセットします。

-   基になるミニポートドライバーに送信される NDIS 呼び出しを行わないでください。ただし、 [**NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)でネットワークデータを返すなどのリソースを返す呼び出しは除きます。

*Protocolstatusex*(または*protocolcostatusex*) が\_エンドメッセージを\_リセットして NDIS\_ステータスを受け取ると、プロトコルドライバーはネットワークデータと OID 要求の送信を再開できます。

 

 





