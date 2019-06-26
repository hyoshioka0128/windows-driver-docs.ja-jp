---
title: 接続指向ミニポート ドライバーの情報の設定
description: 接続指向ミニポート ドライバーの情報の設定
ms.assetid: e31d2054-5982-4ba5-a9e9-133c0d4ed875
keywords:
- 接続指向のドライバー WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc1a11d6877be8450840d405e1543ad6b8eab38a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375147"
---
# <a name="setting-information-for-a-connection-oriented-miniport-driver"></a>接続指向ミニポート ドライバーの情報の設定





バインドされているプロトコルを呼び出し、接続指向のミニポート ドライバーを保持する OID を設定する[ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)渡します、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造を照会して、オブジェクトを設定する必要があります値を格納しているバッファーを指すオブジェクト (OID) を指定します。 呼び出し**NdisCoOidRequest** NDIS ミニポート ドライバーを呼び出すと、 [ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)関数で、指定された値を持つオブジェクトを設定します。

呼び出し**NdisCoOidRequest**同期または非同期で完了できます。 ミニポート ドライバーを呼び出し、呼び出しを非同期的に完了する[ **NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequestcomplete)します。 次の図は、接続指向のミニポート ドライバーの設定情報を示します。

![接続指向のミニポート ドライバーの設定情報を示す図](images/fig5-3.png)

 

 





