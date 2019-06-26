---
title: インターフェイス オブジェクト クエリ要求の処理
description: インターフェイス オブジェクト クエリ要求の処理
ms.assetid: c4dc4d9e-52ea-477f-9bc8-cf04ccaa73b2
keywords:
- NDIS は、ネットワーク インターフェイスの WDK、クエリ要求
- ネットワーク インターフェイス、WDK クエリ要求
- Oid WDK ネットワーク、ネットワーク インターフェイス
- OID 要求 WDK ネットワーク
- クエリは、WDK のネットワー キングを要求します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c43078a26f669bd24d431918cf533e91d2c0c0c3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366632"
---
# <a name="handling-an-interface-object-query-request"></a>インターフェイス オブジェクト クエリ要求の処理





NDIS をインターフェイス オブジェクトに関連付けられている現在の値を取得するには、呼び出しのインターフェイス プロバイダーの[ **ProviderQueryObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-if_query_object)関数。 この関数は、NDIS を返します\_状態\_クエリ要求または、NDIS を正常に処理する場合の成功\_状態\_*Xxx*エラー コードを返します。

インターフェイスのプロバイダーに固有の OID 要求の一覧は、次を参照してください。 [NDIS ネットワーク インターフェイスの Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)します。 NDIS は、プロバイダーを使用している Oid の一覧は、ネットワーク インターフェイスのオブジェクトをサポートするには、ミニポート アダプター、およびフィルター モジュールを参照してください[OID マッピングをネットワーク インターフェイスの NDIS](mapping-of-ndis-network-interfaces-to-ndis-oids.md)します。

ハンドル、 *ProviderIfContext*パラメーターの[ **ProviderQueryObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-if_query_object)インターフェイス プロバイダーは、呼び出されると、NDIS に渡すコンテキスト領域を識別します[ **NdisIfRegisterInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterinterface)インターフェイスを登録する関数。 *ObjectId*パラメーターが照会されるオブジェクトの OID を指定します。 *POutputBufferLength*と*pOutputBuffer*パラメーターは、結果の長さの出力バッファーへのポインターと、出力バッファーへのポインターをそれぞれ提供します。

 

 





