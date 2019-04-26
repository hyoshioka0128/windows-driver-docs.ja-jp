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
ms.openlocfilehash: c2ebc35e7715eaacef425ba7f575c013949df08d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343475"
---
# <a name="mapping-of-guids-to-oids-and-miniport-driver-status"></a>GUID の OID へのマッピングとミニポート ドライバーの状態





WMI がミニポート アダプターに WMI 要求を送信すると (I/O 要求パケットを送信すると、WMI \[IRP\] NDIS を作成する機能のデバイス オブジェクトを)、NDIS は、要求をインターセプトします。 NDIS は、NDIS は要求を処理できる必要があることについては、既にある場合は、ミニポート ドライバーに要求を転送しません。 それ以外の場合、NDIS OID とし、クエリにマップされて WMI GUID または OID を設定します。

NDIS ミニポート ドライバーを呼び出すことができます、ミニポート ドライバーがコネクションレス ミニポート ドライバーの場合は、 [ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416) OID 要求を処理する関数。 NDIS ミニポート ドライバーを呼び出すことができます、ミニポート ドライバーが接続指向のミニポート ドライバーの場合は、 [ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362) OID 要求を処理する関数。 NDIS は、クエリの結果を返しますまたは WMI に要求を設定します。

ミニポート ドライバーで状態インジケーターを生成する、 [ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)または[ **NdisMCoIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563562)関数。 WMI イベントを WMI クライアントを登録し、ミニポート ドライバーが関連付けられている状態を示す値を生成、NDIS は WMI の GUID にその状態を示す値をマップし、WMI に、WMI イベントを示す値を渡します。 WMI は、すべての WMI イベントとして登録されている WMI クライアントに、WMI イベントを示す値を渡します。

 

 





