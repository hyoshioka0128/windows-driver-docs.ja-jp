---
title: インターフェイス オブジェクト クエリ要求の処理
description: インターフェイス オブジェクト クエリ要求の処理
ms.assetid: c4dc4d9e-52ea-477f-9bc8-cf04ccaa73b2
keywords:
- NDIS ネットワークインターフェイス WDK、クエリ要求
- ネットワークインターフェイス WDK、クエリ要求
- Oid WDK ネットワーク、ネットワークインターフェイス
- OID が WDK ネットワークを要求する
- クエリ要求 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e50e7ee63e2f0c8c49234c07b11fdf20a32d312c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842112"
---
# <a name="handling-an-interface-object-query-request"></a>インターフェイス オブジェクト クエリ要求の処理





インターフェイスオブジェクトに関連付けられている現在の値を取得するために、NDIS はインターフェイスプロバイダーの[**Providerqueryobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-if_query_object)関数を呼び出します。 この関数\_は、クエリ要求を正常に処理した場合は NDIS\_STATUS\_SUCCESS を返し、それ以外の場合は\_*Xxx*エラーコードを返します。

インターフェイスプロバイダー固有の OID 要求の一覧については、「 [NDIS Network Interface oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)」を参照してください。 NDIS がプロバイダー、ミニポートアダプター、およびフィルターモジュールを使用してネットワークインターフェイスオブジェクトをサポートする Oid の一覧については、「 [Ndis Network interface TO OID Mapping](mapping-of-ndis-network-interfaces-to-ndis-oids.md)」を参照してください。

[**Providerqueryobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-if_query_object)の*ProviderIfContext*パラメーターにあるハンドルは、インターフェイスプロバイダーがインターフェイスを登録するために[**NdisIfRegisterInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface)関数を呼び出したときに NDIS に渡されたコンテキスト領域を識別します。 *ObjectId*パラメーターは、クエリ対象のオブジェクトの OID を指定します。 *Poutputbufferlength*および*poutputbuffer*パラメーターは、出力バッファーの結果の長さと出力バッファーへのポインターをそれぞれ指すポインターを提供します。

 

 





