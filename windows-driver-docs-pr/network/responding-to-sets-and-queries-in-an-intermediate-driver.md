---
title: 中間ドライバーでの設定およびクエリへの応答
description: 中間ドライバーでの設定およびクエリへの応答
ms.assetid: ccc99542-4a36-4bf9-8a19-4e7d385399da
keywords:
- クエリ操作 WDK NDIS 中間
- WDK NDIS 中間の設定操作
- OID のキャンセルを要求します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a3a355277ba6af9617580361b794f51e9065f7c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378642"
---
# <a name="responding-to-sets-and-queries-in-an-intermediate-driver"></a>中間ドライバーでの設定およびクエリへの応答





クエリとセットからも受信できる、NDIS 中間ドライバは、上位の NDIS ドライバーにバインドするため、その[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)関数。 場合によっては、中間ドライバーはだけを基になるミニポート ドライバーを通じてこのような要求を渡します。 それ以外の場合、これらのクエリに応答でき、メディア、上端にエクスポートするには必要に応じて設定します。 中間のドライバーは、OID を常に渡す必要がありますので注意\_PNP\_*Xxx*基になるミニポート ドライバーに関連付けた NDIS ドライバーから受信した要求。 NDIS 6.0 の中間ドライバーでは、OID 要求はキャンセルもできます。

NDIS ドライバーは、基になるまでの要求を転送するようにドライバー呼び出しが中間[ **NdisAllocateCloneOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatecloneoidrequest)を割り当てる、複製された[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体。 ドライバーの呼び出し、 [ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)要求を送信する関数。 要求が完了したら、ドライバーを呼び出す必要があります、 [ **NdisFreeCloneOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreecloneoidrequest) NDIS の解放関数\_OID\_要求の構造。

OID、要求をキャンセルする、 [ **NdisCancelOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceloidrequest)関数。

通常、中間のドライバーを受信する一般的な Oid は、同じまたは中間のドライバーが基になるミニポート ドライバーに送信するものと似ています。 中間のドライバーを受信するメディアに固有の Oid は、上にあるドライバーを必要とするメディアの種類です。

中間ドライバー自体では、基になるミニポートにセットの要求を渡すのではなく、OID の設定を処理する場合は、設定する値を検証します。 判断した場合、中間のドライバーを設定する値が範囲外である、そのセットの要求は失敗します。

**注**  関数は、ネットワーク データで実行できません中間のドライバーが TCP オフロードを基になるミニポート ドライバーに転送する TCP ネットワーク データの内容を変更する場合は、中間のドライバーにする必要があります応答[OID\_TCP\_オフロード\_現在\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config) NDIS の状態を持つクエリ\_状態\_いない\_サポートされています。代わりに、ミニポートを基になるまで、要求を渡します。

 

セットと、中間ドライバーでのクエリに応答する方法の詳細については、次を参照してください。[取得し、ミニポート ドライバー情報の設定と、WMI の NDIS サポート](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)します。

 

 





