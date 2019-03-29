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
ms.openlocfilehash: 072a9df35fced3723389e304ce4d0b59df5457dd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570993"
---
# <a name="responding-to-sets-and-queries-in-an-intermediate-driver"></a>中間ドライバーでの設定およびクエリへの応答





クエリとセットからも受信できる、NDIS 中間ドライバは、上位の NDIS ドライバーにバインドするため、その[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)関数。 場合によっては、中間ドライバーはだけを基になるミニポート ドライバーを通じてこのような要求を渡します。 それ以外の場合、これらのクエリに応答でき、メディア、上端にエクスポートするには必要に応じて設定します。 中間のドライバーは、OID を常に渡す必要がありますので注意\_PNP\_*Xxx*基になるミニポート ドライバーに関連付けた NDIS ドライバーから受信した要求。 NDIS 6.0 の中間ドライバーでは、OID 要求はキャンセルもできます。

NDIS ドライバーは、基になるまでの要求を転送するようにドライバー呼び出しが中間[ **NdisAllocateCloneOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff560706)を割り当てる、複製された[ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体。 ドライバーの呼び出し、 [ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)要求を送信する関数。 要求が完了したら、ドライバーを呼び出す必要があります、 [ **NdisFreeCloneOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561845) NDIS の解放関数\_OID\_要求の構造。

OID、要求をキャンセルする、 [ **NdisCancelOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561622)関数。

通常、中間のドライバーを受信する一般的な Oid は、同じまたは中間のドライバーが基になるミニポート ドライバーに送信するものと似ています。 中間のドライバーを受信するメディアに固有の Oid は、上にあるドライバーを必要とするメディアの種類です。

中間ドライバー自体では、基になるミニポートにセットの要求を渡すのではなく、OID の設定を処理する場合は、設定する値を検証します。 判断した場合、中間のドライバーを設定する値が範囲外である、そのセットの要求は失敗します。

**注**  関数は、ネットワーク データで実行できません中間のドライバーが TCP オフロードを基になるミニポート ドライバーに転送する TCP ネットワーク データの内容を変更する場合は、中間のドライバーにする必要があります応答[OID\_TCP\_オフロード\_現在\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569805) NDIS の状態を持つクエリ\_状態\_いない\_サポートされています。代わりに、ミニポートを基になるまで、要求を渡します。

 

セットと、中間ドライバーでのクエリに応答する方法の詳細については、次を参照してください。[取得し、ミニポート ドライバー情報の設定と、WMI の NDIS サポート](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)します。

 

 





