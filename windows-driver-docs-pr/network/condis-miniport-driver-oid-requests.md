---
title: CoNDIS ミニポート ドライバー OID 要求
description: CoNDIS ミニポート ドライバー OID 要求
ms.assetid: a283d430-f90c-4704-868b-f4086922737b
keywords:
- ミニポート ドライバー WDK ネットワー キング、いる CoNDIS
- NDIS ミニポート ドライバー WDK、いる CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61ebc76b73a9e648991c6189cda319371b61dd2b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570736"
---
# <a name="condis-miniport-driver-oid-requests"></a>CoNDIS ミニポート ドライバー OID 要求





NDIS は呼び出している CoNDIS ミニポート ドライバーの[ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)クエリまたはドライバーの情報を設定する OID 要求を送信する関数。 NDIS 呼び出し*MiniportCoOidRequest*自身が代理として、または呼び出される上位のドライバーに代わって、 [ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)関数。

NDIS 渡します*MiniportCoOidRequest*へのポインター、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)要求情報を含む構造体。 要求の構造には、OID が含まれています。\_*Xxx*要求データを定義するには、要求とその他のメンバーの種類を示す識別子です。

**タイムアウト**メンバーは、秒単位の要求で、タイムアウトを指定します。 NDIS は、ドライバーをリセットしたり、ドライバーは、要求を完了する前にタイムアウトに達すると、要求をキャンセルできます。

**RequestId**メンバーは、要求のオプションの識別子を指定します。 ミニポート ドライバーを設定できる、 **RequestId**ドライバーがから取得した値に状態表示のメンバー、 **RequestId**関連付けられている OID 要求のメンバー。 通常、ミニポート ドライバーでは、このメンバーを無視できます。 ドライバーは、このメンバーを設定する必要がある場合、ドライバーは、特定の OID のリファレンス ページで指定された必要な値のいずれかを使用する必要があります。 状態インジケーターの詳細については、[いる CoNDIS ミニポート ドライバーの状態インジケーター](condis-miniport-driver-status-indications.md)を参照してください。

ミニポート ドライバーは、成功または失敗の状態を返すことによって、OID 要求を同期的に完了できます。 ドライバーは NDIS を返すことによって、OID 要求を非同期的に実行できる\_状態\_保留します。 この場合、ドライバーを呼び出す必要があります、 [ **NdisMCoOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563568)操作を完了する関数。

場合、 *MiniportCoOidRequest*返します NDIS\_状態\_保留中、NDIS を呼び出すことができます*MiniportCoOidRequest*別の要求をする前に、アダプターで、保留中要求が完了したとします。 これは OID のすべての要求がシリアル化、コネクションレスの NDIS インターフェイスを異なることに注意してください。

NDIS ミニポート ドライバーを呼び出すことができます[ *MiniportCancelOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559339)いる CoNDIS OID 要求をキャンセルする関数。

 

 





