---
title: GUID の OID へのマッピングとミニポート ドライバーの状態
description: GUID の OID へのマッピングとミニポート ドライバーの状態
ms.assetid: b3c9bb40-2906-4059-b9fa-06f6ababd3f2
keywords:
- WMI の WDK にネットワーク接続、Guid
- Oid WDK ネットワー キング、WMI
- Guid の WDK ネットワーク
- Windows Management Instrumentation の WDK ネットワー キング、Guid
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97fd94e974bb0aa0021130997690b7531bdb2349
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369172"
---
# <a name="mapping-of-guids-to-oids-and-miniport-driver-status"></a>GUID の OID へのマッピングとミニポート ドライバーの状態





WMI がミニポート アダプターに WMI 要求を送信すると (I/O 要求パケットを送信すると、WMI \[IRP\] NDIS を作成する機能のデバイス オブジェクトを)、NDIS は、要求をインターセプトします。 NDIS は、NDIS は要求を処理できる必要があることについては、既にある場合は、ミニポート ドライバーに要求を転送しません。 それ以外の場合、NDIS OID とし、クエリにマップされて WMI GUID または OID を設定します。

NDIS ミニポート ドライバーを呼び出すことができます、ミニポート ドライバーがコネクションレス ミニポート ドライバーの場合は、 [ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request) OID 要求を処理する関数。 NDIS ミニポート ドライバーを呼び出すことができます、ミニポート ドライバーが接続指向のミニポート ドライバーの場合は、 [ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request) OID 要求を処理する関数。 NDIS は、クエリの結果を返しますまたは WMI に要求を設定します。

ミニポート ドライバーで状態インジケーターを生成する、 [ **NdisMIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)または[ **NdisMCoIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatestatusex)関数。 WMI イベントを WMI クライアントを登録し、ミニポート ドライバーが関連付けられている状態を示す値を生成、NDIS は WMI の GUID にその状態を示す値をマップし、WMI に、WMI イベントを示す値を渡します。 WMI は、すべての WMI イベントとして登録されている WMI クライアントに、WMI イベントを示す値を渡します。

 

 





