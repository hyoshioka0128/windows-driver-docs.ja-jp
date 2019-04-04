---
title: 要求の設定、インターフェイス オブジェクトの処理
description: 要求の設定、インターフェイス オブジェクトの処理
ms.assetid: aed27b0b-fff5-4e9f-b368-526a8bf79c59
keywords:
- NDIS は、ネットワーク インターフェイスの WDK、要求の設定
- ネットワーク インターフェイスの WDK、要求の設定
- Oid WDK ネットワーク、ネットワーク インターフェイス
- OID 要求 WDK ネットワーク
- 要求の WDK ネットワークを設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1aea81421cd2d09ef7461c782b8920835183e05
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527609"
---
# <a name="handling-an-interface-object-set-request"></a>要求の設定、インターフェイス オブジェクトの処理


インターフェイス オブジェクトに関連付けられているデータを設定するには NDIS からインターフェイス プロバイダーが呼び出さ[ **ProviderSetObject** ](https://msdn.microsoft.com/library/windows/hardware/ff570403)関数。 NDIS を返します\_状態\_データや、NDIS 正常に変更された場合の成功\_状態\_*Xxx*エラー コードを返します。

インターフェイスのプロバイダーに固有の OID 要求の一覧は、[NDIS ネットワーク インターフェイスの Oid](https://msdn.microsoft.com/library/windows/hardware/ff566545)を参照してください。 NDIS は、プロバイダーを使用している Oid の一覧は、ネットワーク インターフェイスのオブジェクトをサポートするには、ミニポート アダプター、およびフィルター モジュールを参照してください[OID マッピングをネットワーク インターフェイスの NDIS](mapping-of-ndis-network-interfaces-to-ndis-oids.md)します。

ハンドル、 *ProviderIfContext*パラメーターの[ **ProviderSetObject** ](https://msdn.microsoft.com/library/windows/hardware/ff570403)インターフェイス プロバイダーは、呼び出されると、NDIS に渡すコンテキスト領域を識別します[ **NdisIfRegisterInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff562715)インターフェイスを登録する関数。 *ObjectId*パラメーターが設定されるオブジェクトの OID を指定します。 *InputBufferLength*と*pInputBuffer*パラメーターはそれぞれ、入力バッファーと、入力バッファーへのポインターの長さを提供します。

 

 





