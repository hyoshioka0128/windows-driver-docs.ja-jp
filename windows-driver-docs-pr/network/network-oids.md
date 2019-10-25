---
title: ネットワーク OID
description: ネットワーク OID
ms.assetid: a897ba37-7984-455f-9428-a74850f7e3b6
keywords:
- Oid WDK ネットワーク
- ネットワーク Oid WDK
- オブジェクト識別子 WDK ネットワーク
- Oid WDK ネットワーク, Oid について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3431c188122a147a7a5b2e9812f39646f8eb81d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827133"
---
# <a name="network-oids"></a>ネットワーク OID





ミニポートドライバーでは、その機能と現在の状態に関する情報に加え、管理する各ミニポートアダプターに関する情報も保持されます。 各情報の種類は、オブジェクト識別子 (OID) によって識別されます。 Oid はシステムで定義されています。 NDIS はミニポートドライバーに対する多くの OID 要求を処理し、NDIS はそのような要求をミニポートドライバーに渡しません。 ミニポートドライバーは、初期化中に OID クエリに応答して報告された機能の多くを、属性の属性で報告します。 レポート属性の詳細については、「[アダプターの初期化](initializing-a-miniport-adapter.md)」を参照してください。

NDIS およびそれ以降のレベルのドライバーでは、Oid を使用してクエリを実行したり、場合によっては情報を設定したりできます。

-   コネクションレスメディアの上位レベルのドライバーは、コネクションレスのミニポートドライバーの情報を照会または設定する[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)を呼び出します。 クエリまたは設定操作を実行するために、NDIS はミニポートドライバーの[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数を呼び出します。

-   接続指向のミニポートドライバーで情報を照会したり設定したりするための、より高いレベルの接続指向メディア呼び出し[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest) 。 クエリと設定の両方の操作を実行するために、NDIS はミニポートドライバーの[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)関数を呼び出します。

NDIS は、ミニポートドライバー用のシステム定義 Oid の多くをグローバル一意識別子 (Guid) にマップします。 NDIS は、これらの Guid を、ユーザーモード Web-Based Enterprise Management (WBEM) アプリケーションをサポートするカーネルモードの Microsoft Windows Management Instrumentation (WMI) に登録します。 WMI クライアントがこれらの Guid のいずれかを照会または設定すると、NDIS は必要に応じて要求をクエリ OID 操作または設定 OID 操作に変換し、返された情報とステータスを WMI に渡します。 カスタム Guid をカスタム Oid またはミニポートドライバーの状態にマップすることができます。 ミニポートドライバーは、初期化時に、NDIS を使用して、カスタムの GUID から OID または GUID から状態へのマッピングを登録する必要があります。

Oid の照会と設定、カスタム Oid の作成、WMI の NDIS サポートの詳細については、「[ミニポートドライバー情報の取得と設定」および「wmi の ndis](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)サポート」を参照してください。

 

 





