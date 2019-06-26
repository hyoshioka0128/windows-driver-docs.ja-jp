---
title: プロトコル ドライバー OID 要求
description: プロトコル ドライバー OID 要求
ms.assetid: ab664e75-d17d-4664-8c37-91fd651d23c2
keywords:
- プロトコル ドライバー WDK ネットワーク、OID 要求
- Oid WDK ネットワー キング、プロトコル ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7ae0350e5a600c1c253fd29233d51a5e3caa317
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385455"
---
# <a name="protocol-driver-oid-requests"></a>プロトコル ドライバー OID 要求





NDIS は、デバイスの特性、構成可能な設定、および統計情報などのパラメーターを含むアダプターのパラメーターを識別するためにオブジェクト識別子 (OID) の値を定義します。 Oid の詳細については、次を参照してください。 [NDIS Oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

プロトコル ドライバーでは、クエリを実行したり、基になるドライバーの動作のパラメーターを設定することができます。

NDIS も用意されています。、 [NDIS 6.1 の OID 要求インターフェイスを直接](direct-oid-request-interface-in-ndis-6-1.md)プロトコル ドライバー。 *OID の直接の要求パス*クエリを実行したり、頻繁に設定されている OID 要求をサポートします。 IPsec のバージョン 2 (IPsecv2) オフロードなどのインターフェイスを提供、 [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa)直接 OID 要求の OID。 直接の OID 要求インターフェイスは、NDIS ドライバーでは省略可能。

プロトコル ドライバー OID 要求の詳細については、以下のトピックです。

[NDIS プロトコル ドライバーから OID 要求を生成します。](generating-oid-requests-from-an-ndis-protocol-driver.md)

[ドライバーの OID を直接要求するプロトコル](protocol-driver-direct-oid-requests.md)

[プロトコル ドライバーの同期の OID を要求](protocol-driver-synchronous-oid-requests.md)

 

 





