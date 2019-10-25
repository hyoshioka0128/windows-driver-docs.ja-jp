---
title: 接続指向ミニポート ドライバーの情報の設定
description: 接続指向ミニポート ドライバーの情報の設定
ms.assetid: e31d2054-5982-4ba5-a9e9-133c0d4ed875
keywords:
- 接続指向ドライバー WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8be8e0180e640ab4a41a9ee139f3a1dd187a1a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841945"
---
# <a name="setting-information-for-a-connection-oriented-miniport-driver"></a>接続指向ミニポート ドライバーの情報の設定





接続指向のミニポートドライバーによって保持される OID を設定するために、バインドされたプロトコルは[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)を呼び出し、クエリ対象のオブジェクト (oid) を指定する[ **\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造を渡します。オブジェクトを設定する必要がある値を格納しているバッファー。 **NdisCoOidRequest**を呼び出すと、NDIS はミニポートドライバーの[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)関数を呼び出します。これにより、オブジェクトに指定された値が設定されます。

**NdisCoOidRequest**の呼び出しは、同期的または非同期的に完了できます。 呼び出しを非同期に完了するために、ミニポートドライバーは[**NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequestcomplete)を呼び出します。 次の図は、接続指向ミニポートドライバーでの情報の設定を示しています。

![接続指向ミニポートドライバーでの設定情報を示す図](images/fig5-3.png)

 

 





