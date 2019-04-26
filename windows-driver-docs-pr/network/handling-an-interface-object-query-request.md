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
ms.openlocfilehash: fd2909df9c04a23d7eecd7726dad76b191b1827e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349750"
---
# <a name="handling-an-interface-object-query-request"></a>インターフェイス オブジェクト クエリ要求の処理





NDIS をインターフェイス オブジェクトに関連付けられている現在の値を取得するには、呼び出しのインターフェイス プロバイダーの[ **ProviderQueryObject** ](https://msdn.microsoft.com/library/windows/hardware/ff570399)関数。 この関数は、NDIS を返します\_状態\_クエリ要求または、NDIS を正常に処理する場合の成功\_状態\_*Xxx*エラー コードを返します。

インターフェイスのプロバイダーに固有の OID 要求の一覧は、次を参照してください。 [NDIS ネットワーク インターフェイスの Oid](https://msdn.microsoft.com/library/windows/hardware/ff566545)します。 NDIS は、プロバイダーを使用している Oid の一覧は、ネットワーク インターフェイスのオブジェクトをサポートするには、ミニポート アダプター、およびフィルター モジュールを参照してください[OID マッピングをネットワーク インターフェイスの NDIS](mapping-of-ndis-network-interfaces-to-ndis-oids.md)します。

ハンドル、 *ProviderIfContext*パラメーターの[ **ProviderQueryObject** ](https://msdn.microsoft.com/library/windows/hardware/ff570399)インターフェイス プロバイダーは、呼び出されると、NDIS に渡すコンテキスト領域を識別します[ **NdisIfRegisterInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff562715)インターフェイスを登録する関数。 *ObjectId*パラメーターが照会されるオブジェクトの OID を指定します。 *POutputBufferLength*と*pOutputBuffer*パラメーターは、結果の長さの出力バッファーへのポインターと、出力バッファーへのポインターをそれぞれ提供します。

 

 





