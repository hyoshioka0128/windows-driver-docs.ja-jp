---
title: インターフェイス オブジェクト設定要求の処理
description: インターフェイス オブジェクト設定要求の処理
ms.assetid: aed27b0b-fff5-4e9f-b368-526a8bf79c59
keywords:
- NDIS は、ネットワーク インターフェイスの WDK、要求の設定
- ネットワーク インターフェイスの WDK、要求の設定
- Oid WDK ネットワーク、ネットワーク インターフェイス
- OID 要求 WDK ネットワーク
- 要求の WDK ネットワークを設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5490124d6aacac6018d3846709813b58b0011dcd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371236"
---
# <a name="handling-an-interface-object-set-request"></a>インターフェイス オブジェクト設定要求の処理


インターフェイス オブジェクトに関連付けられているデータを設定するには NDIS からインターフェイス プロバイダーが呼び出さ[ **ProviderSetObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-if_set_object)関数。 NDIS を返します\_状態\_データや、NDIS 正常に変更された場合の成功\_状態\_*Xxx*エラー コードを返します。

インターフェイスのプロバイダーに固有の OID 要求の一覧は、次を参照してください。 [NDIS ネットワーク インターフェイスの Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)します。 NDIS は、プロバイダーを使用している Oid の一覧は、ネットワーク インターフェイスのオブジェクトをサポートするには、ミニポート アダプター、およびフィルター モジュールを参照してください[OID マッピングをネットワーク インターフェイスの NDIS](mapping-of-ndis-network-interfaces-to-ndis-oids.md)します。

ハンドル、 *ProviderIfContext*パラメーターの[ **ProviderSetObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-if_set_object)インターフェイス プロバイダーは、呼び出されると、NDIS に渡すコンテキスト領域を識別します[ **NdisIfRegisterInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterinterface)インターフェイスを登録する関数。 *ObjectId*パラメーターが設定されるオブジェクトの OID を指定します。 *InputBufferLength*と*pInputBuffer*パラメーターはそれぞれ、入力バッファーと、入力バッファーへのポインターの長さを提供します。

 

 





