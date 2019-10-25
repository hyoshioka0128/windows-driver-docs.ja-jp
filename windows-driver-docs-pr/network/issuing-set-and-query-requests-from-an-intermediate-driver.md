---
title: 中間ドライバーからの設定およびクエリ要求の発行
description: 中間ドライバーからの設定およびクエリ要求の発行
ms.assetid: bd049639-970c-43c8-8ef9-c5e75cc2d75f
keywords:
- クエリ操作 WDK NDIS 中間
- set 操作 WDK NDIS 中間
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62005faeceebc27d891eb250e5ac31ac884fa762
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844150"
---
# <a name="issuing-set-and-query-requests-from-an-intermediate-driver"></a>中間ドライバーからの設定およびクエリ要求の発行





中間ドライバーのプロトコルエッジは、基になるミニポートドライバーに設定およびクエリ情報要求を発行できます。 中間ドライバーの仮想ミニポートエッジは、基になるドライバーから取得した情報を使用して、設定要求およびクエリ要求への応答方法を決定できます。

OID 要求を取り消すには、 [**NdisCancelOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceloidrequest)関数を呼び出します。

設定およびクエリ要求への応答の詳細については、「[中間ドライバーでのセットおよびクエリへの応答](responding-to-sets-and-queries-in-an-intermediate-driver.md)」を参照してください。 OID 要求の発行の詳細については、「[プロトコルドライバーでの Oid 要求操作](oid-request-operations-in-a-protocol-driver.md)」を参照してください。

 

 





