---
title: OID_CO_ADDRESS_CHANGE
description: このトピックでは、OID_CO_ADDRESS_CHANGE オブジェクト識別子 (OID) について説明します。
ms.assetid: 18b185dd-b282-4182-a761-008e5d0c88d7
keywords:
- OID_CO_ADDRESS_CHANGE
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e91da29223d4ccde274d137f6c7dc2f8a1c1da9
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918200"
---
# <a name="oid_co_address_change"></a>OID_CO_ADDRESS_CHANGE

OID_CO_ADDRESS_CHANGE OID は、コールマネージャーによって、通話マネージャーを使用してアドレスファミリを開いた各クライアントに送信されます。 このアクションは、呼び出しマネージャーが使用するスイッチアドレスの変更に応答して実行されます。 たとえば、だれかが1つのスイッチから NIC を切断し、別のスイッチに接続した場合、呼び出しマネージャーはこの要求を送信します。 通知された各クライアントは、OID_CO_GET_ADDRESSES クエリを呼び出しマネージャーに送信して、現在有効なアドレスの一覧を取得する必要があります。

また、コールマネージャーは、クライアントが呼び出しマネージャーでアドレスファミリを開いた直後に、クライアントに OID_CO_ADDRESS_CHANGE を送信します。 これにより、スイッチアドレスが変更された後にアドレスファミリを開くクライアントが変更を通知されるようになります。 その後、クライアントは OID_CO_GET_ADDRESSES クエリを呼び出しマネージャーに送信する必要があります。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

