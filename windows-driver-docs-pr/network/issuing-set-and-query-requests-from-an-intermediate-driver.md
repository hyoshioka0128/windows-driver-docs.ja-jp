---
title: 発行元のセットと、中間ドライバーからのクエリ要求
description: 発行元のセットと、中間ドライバーからのクエリ要求
ms.assetid: bd049639-970c-43c8-8ef9-c5e75cc2d75f
keywords:
- クエリ操作 WDK NDIS 中間
- WDK NDIS 中間の設定操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54c843dae6ddbea99e3d7c128004b0f05aabe3a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556657"
---
# <a name="issuing-set-and-query-requests-from-an-intermediate-driver"></a>発行元のセットと、中間ドライバーからのクエリ要求





中間のドライバーのプロトコルの端では、セットを発行でき、基になるミニポート ドライバーに情報の要求のクエリを実行することができます。 中間のドライバーの仮想ミニポート edge は、基になるドライバーから取得した情報を使用して、設定に応答する方法とクエリ要求を決定できます。

OID、要求をキャンセルする、 [ **NdisCancelOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561622)関数。

設定し、クエリ要求の応答の詳細については、[セットと、中間ドライバーでのクエリに対応する](responding-to-sets-and-queries-in-an-intermediate-driver.md)を参照してください。 OID の要求を発行の詳細については、[プロトコル ドライバーに OID 要求操作](oid-request-operations-in-a-protocol-driver.md)を参照してください。

 

 





