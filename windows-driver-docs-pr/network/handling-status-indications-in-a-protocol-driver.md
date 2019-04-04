---
title: プロトコル ドライバーに状態インジケーターの処理
description: プロトコル ドライバーに状態インジケーターの処理
ms.assetid: 1a021919-fd27-49b2-95a0-5ccb9029abd4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5eba1b6cc8279c844ed15e36f14c43879cab2679
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557741"
---
# <a name="handling-status-indications-in-a-protocol-driver"></a>プロトコル ドライバーに状態インジケーターの処理





プロトコル ドライバーを指定する必要があります、 [ **ProtocolStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff570270) NDIS が、基になるドライバーの状態を報告したときに呼び出す関数です。

NDIS 呼び出しプロトコル ドライバーの*ProtocolStatusEx*関数は、状態を示す値の関数を呼び出して、基になるドライバーから ([**NdisMIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff553538)または[ **NdisFIndicateStatus**](https://msdn.microsoft.com/library/windows/hardware/ff561824))。 詳細については、ミニポート ドライバーからの状態を示す、[アダプター状態のインジケーター](miniport-adapter-status-indications.md)を参照してください。

詳細については、フィルター ドライバーからの状態を示す、[フィルター モジュールの状態インジケーター](filter-module-status-indications.md)を参照してください。

状態の表示が OID 要求に関連付けられている場合は、基になるドライバーを設定できます、 **DestinationHandle**と**RequestId**その NDIS は、特定の状態の表示を提供できるように、メンバープロトコル バインディング。 OID 要求の詳細については、[プロトコル ドライバー OID 要求](protocol-driver-oid-requests.md)を参照してください。

 

 





