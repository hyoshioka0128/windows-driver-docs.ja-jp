---
title: OID_CO_ADDRESS_CHANGE
description: このトピックでは、OID_CO_ADDRESS_CHANGE オブジェクト識別子 (OID) について説明します。
ms.assetid: 18b185dd-b282-4182-a761-008e5d0c88d7
keywords:
- OID_CO_ADDRESS_CHANGE
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 057575360289eacbabdac36ca2356e9d91d86382
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560197"
---
# <a name="oidcoaddresschange"></a>OID_CO_ADDRESS_CHANGE

OID_CO_ADDRESS_CHANGE OID は、コール マネージャーによってコール マネージャーで、アドレス ファミリをオープンした各クライアントに送信されます。 この操作は、コール マネージャーを使用するスイッチのアドレスの変更に応答で実行されます。 たとえば、コール マネージャーは、NIC を 1 つのスイッチから切断別のスイッチに接続されるため、ユーザーがいる場合、この要求を送信します。 通知された各クライアントでは、現在有効なアドレスの一覧を取得する呼び出しのマネージャーに OID_CO_GET_ADDRESSES クエリを送信する必要があります。

コール マネージャーは、クライアントは、コール マネージャーで、アドレス ファミリを開いた後にすぐにも OID_CO_ADDRESS_CHANGE とクライアントに送信します。 これにより、変更のスイッチのアドレスが変更された後、アドレス ファミリを表示するクライアントに通知します。 クライアントする必要がありますしする必要がありますし、クエリを送信 OID_CO_GET_ADDRESSES コール マネージャーにします。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

