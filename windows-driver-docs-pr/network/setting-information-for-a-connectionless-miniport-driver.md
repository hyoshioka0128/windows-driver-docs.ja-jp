---
title: コネクションレス ミニポート ドライバーの情報の設定
description: コネクションレス ミニポート ドライバーの情報の設定
ms.assetid: 406d844a-cc83-4cd6-a2d2-78e614aab900
keywords:
- コネクションレス ドライバー WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c4fa72085c28b1e5961d6cbc6be9c4f83492346
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375157"
---
# <a name="setting-information-for-a-connectionless-miniport-driver"></a>コネクションレス ミニポート ドライバーの情報の設定





バインドされているプロトコルを呼び出すコネクションレス ミニポート ドライバーを保持する OID を設定する[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)渡します、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造を照会して、オブジェクトを設定する必要があります値を格納しているバッファーを指すオブジェクト (OID) を指定します。 呼び出し**NdisOidRequest** NDIS ミニポート ドライバーを呼び出すと、 [ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)関数で、指定された値を持つオブジェクトを設定します。

呼び出し*MiniportOidRequest*同期または非同期で完了できます。 ミニポート ドライバーを呼び出し、呼び出しを非同期的に完了する[ **NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismoidrequestcomplete)します。 次の図は、(バインド) ごとのコネクションレス ミニポート ドライバーでの設定情報を示します。

![(バインド) ごとのコネクションレス ミニポート ドライバーでの設定情報を示す図](images/fig5-4.png)

 

 





