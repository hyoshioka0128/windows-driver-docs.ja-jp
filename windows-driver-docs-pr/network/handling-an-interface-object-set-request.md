---
title: インターフェイスオブジェクトセットの要求の処理
description: インターフェイスオブジェクトセットの要求の処理
ms.assetid: aed27b0b-fff5-4e9f-b368-526a8bf79c59
keywords:
- NDIS ネットワークインターフェイス WDK、set requests
- ネットワークインターフェイス WDK、set requests
- Oid WDK ネットワーク、ネットワークインターフェイス
- OID が WDK ネットワークを要求する
- set 要求の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d4d50cfb96817b164d72e96cc3742043361e7bb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842110"
---
# <a name="handling-an-interface-object-set-request"></a>インターフェイスオブジェクトセットの要求の処理


インターフェイスオブジェクトに関連付けられているデータを設定するために、NDIS はインターフェイスプロバイダーの[**ProviderSetObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-if_set_object)関数を呼び出します。 データまたは NDIS\_の\_状態を正常に変更した場合、この関数は NDIS\_STATUS\_SUCCESS を返します。それ以外の場合は、 *Xxx*エラーコードを返します。

インターフェイスプロバイダー固有の OID 要求の一覧については、「 [NDIS Network Interface oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)」を参照してください。 NDIS がプロバイダー、ミニポートアダプター、およびフィルターモジュールを使用してネットワークインターフェイスオブジェクトをサポートする Oid の一覧については、「 [Ndis Network interface TO OID Mapping](mapping-of-ndis-network-interfaces-to-ndis-oids.md)」を参照してください。

[**ProviderSetObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-if_set_object)の*ProviderIfContext*パラメーターにあるハンドルは、インターフェイスプロバイダーがインターフェイスを登録するために[**NdisIfRegisterInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface)関数を呼び出したときに NDIS に渡されたコンテキスト領域を識別します。 *ObjectId*パラメーターは、設定されるオブジェクトの OID を指定します。 *Inputbufferlength*パラメーターと*pinputbuffer*パラメーターは、入力バッファーの長さと入力バッファーへのポインターをそれぞれ提供します。

 

 





