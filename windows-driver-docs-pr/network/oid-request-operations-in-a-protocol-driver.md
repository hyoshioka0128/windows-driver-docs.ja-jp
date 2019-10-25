---
title: プロトコル ドライバーの OID 要求操作
description: プロトコル ドライバーの OID 要求操作
ms.assetid: 767252a2-98de-4df2-89dc-ee48b2c7ca9d
keywords:
- プロトコルドライバー WDK ネットワーク, OID 要求
- NDIS プロトコルドライバー WDK、OID 要求
- OID が WDK ネットワークを要求する
- Oid WDK ネットワーク, プロトコルドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45bb1bc83a95e36a36adfa4d7f8b4622b0fef0c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844003"
---
# <a name="oid-request-operations-in-a-protocol-driver"></a>プロトコル ドライバーの OID 要求操作





プロトコルドライバーの OID 要求操作には、2つの異なるインターフェイスがあります。 コネクションレスの下位エッジを持つ NDIS プロトコルドライバーは、 [**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)関数を呼び出して OID 要求を開始します。 コネクションレスの下端がある NDIS プロトコルドライバーは、 [**ProtocolOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_oid_request_complete)関数を提供する必要があります。 基になるドライバーが保留中の OID 要求を完了すると、NDIS は*ProtocolOidRequestComplete*を呼び出します。 コネクションレスプロトコルドライバーでの OID 要求の詳細については、「[プロトコルドライバー OID 要求](protocol-driver-oid-requests.md)」を参照してください。

接続指向 NDIS (CoNDIS プロトコルドライバーは、 [**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)関数を呼び出して OID 要求を開始します。 CoNDIS プロトコルドライバーは、 [**ProtocolCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request_complete)関数を提供する必要があります。 基になるドライバーが保留中の OID 要求を完了すると、NDIS は*ProtocolOidRequestComplete*を呼び出します。 接続指向プロトコルドライバーでの OID 要求の詳細については、「[接続指向の操作](connection-oriented-operations.md)」を参照してください。

Oid の詳細については、「 [NDIS oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

 

 





