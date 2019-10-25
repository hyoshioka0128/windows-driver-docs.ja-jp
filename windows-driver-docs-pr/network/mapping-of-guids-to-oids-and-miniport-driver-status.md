---
title: GUID の OID へのマッピングとミニポート ドライバーの状態
description: GUID の OID へのマッピングとミニポート ドライバーの状態
ms.assetid: b3c9bb40-2906-4059-b9fa-06f6ababd3f2
keywords:
- WMI WDK ネットワーク, Guid
- Oid WDK ネットワーク、WMI
- Guid WDK ネットワーク
- Windows Management Instrumentation WDK ネットワーク、Guid
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 713984abb5d52e56321c3d55e1c3b420ca0df9c1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844305"
---
# <a name="mapping-of-guids-to-oids-and-miniport-driver-status"></a>GUID の OID へのマッピングとミニポート ドライバーの状態





Wmi がミニポートアダプターに WMI 要求を送信する場合 (つまり、WMI が i/o 要求パケット \[IRP\] を NDIS が作成した機能デバイスオブジェクトに送信する場合) は、NDIS によって要求がインターセプトされます。 Ndis は、要求を処理するために必要な情報を NDIS が既に持っている場合、ミニポートドライバーに要求を転送しません。 それ以外の場合、NDIS は WMI GUID を OID にマップしてから、OID を照会または設定します。

ミニポートドライバーがコネクションレスのミニポートドライバーである場合、NDIS は、ミニポートドライバーの[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数を呼び出して OID 要求を処理できます。 ミニポートドライバーが接続指向のミニポートドライバーである場合、NDIS は、ミニポートドライバーの[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)関数を呼び出して、OID 要求を処理できます。 NDIS は、クエリまたは set 要求の結果を WMI に返します。

ミニポートドライバーは、 [**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)関数または[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)関数を使用してステータスの兆候を生成します。 Wmi クライアントが WMI イベントに登録され、ミニポートドライバーが関連するステータス表示を生成した場合、NDIS はその状態を WMI GUID にマップし、wmi イベントを wmi に渡します。 Wmi は、wmi イベントに対して登録されているすべての WMI クライアントに WMI イベント通知を渡します。

 

 





