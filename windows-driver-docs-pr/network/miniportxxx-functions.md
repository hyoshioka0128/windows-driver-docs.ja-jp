---
title: MiniportXxx 関数
description: MiniportXxx 関数
ms.assetid: b992c3ff-deb1-49e2-a99f-310cc4cb81c3
keywords:
- MiniportXxx functions WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cba2c13efb2c3768cef0b8e1d1edaa56dd908a40
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844229"
---
# <a name="miniportxxx-functions"></a>MiniportXxx 関数





一般的なミニポートドライバーでは、いくつかの関数を使用して、NDIS を介して上位のレイヤーおよびハードウェアと通信します。 これらの関数のすべてが必要なわけではありません。 必須の関数とその理由の詳細については、「[ミニポートドライバーの初期化](initializing-a-miniport-driver.md)」を参照してください。

Ndis ミニポートドライバーおよび上位層ドライバーは、ndis ライブラリ (Ndis) を使用して、ndis *** Xxx*** 関数の呼び出しによって相互に通信します。

多くのミニポートドライバー関数は、同期的または非同期的に動作できます。 非同期関数には、操作の完了時に呼び出す必要がある**Ndis*Xxx*の完全な**関数があります。 たとえば、プロトコルドライバーが[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)を呼び出してミニポートドライバー情報を照会する場合、ミニポートドライバーの*Miniportoidrequest*関数は、NDIS\_STATUS\_PENDING を返すことによってリセット操作を保留できます。 最終的に、ミニポートドライバーは[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)を呼び出して、クエリ要求の最終ステータスを示す必要があります。

 

 





