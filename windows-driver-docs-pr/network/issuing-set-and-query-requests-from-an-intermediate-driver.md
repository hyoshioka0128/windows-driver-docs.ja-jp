---
title: 中間ドライバーからの設定およびクエリ要求の発行
description: 中間ドライバーからの設定およびクエリ要求の発行
ms.assetid: bd049639-970c-43c8-8ef9-c5e75cc2d75f
keywords:
- クエリ操作 WDK NDIS 中間
- WDK NDIS 中間の設定操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f538bf67aa6865f269b5e3630d5c24ff40a1fc7a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356247"
---
# <a name="issuing-set-and-query-requests-from-an-intermediate-driver"></a>中間ドライバーからの設定およびクエリ要求の発行





中間のドライバーのプロトコルの端では、セットを発行でき、基になるミニポート ドライバーに情報の要求のクエリを実行することができます。 中間のドライバーの仮想ミニポート edge は、基になるドライバーから取得した情報を使用して、設定に応答する方法とクエリ要求を決定できます。

OID、要求をキャンセルする、 [ **NdisCancelOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceloidrequest)関数。

設定し、クエリ要求の応答の詳細については、次を参照してください。[セットと、中間ドライバーでのクエリに対応する](responding-to-sets-and-queries-in-an-intermediate-driver.md)します。 OID の要求を発行の詳細については、次を参照してください。[プロトコル ドライバーに OID 要求操作](oid-request-operations-in-a-protocol-driver.md)します。

 

 





