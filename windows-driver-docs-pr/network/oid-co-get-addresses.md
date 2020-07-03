---
title: OID_CO_GET_ADDRESSES
description: このトピックでは、OID_CO_GET_ADDRESSES オブジェクト識別子 (OID) について説明します。
ms.assetid: 0c30e184-be01-49ab-b9ad-3ccc2fdf9fc5
keywords:
- OID_CO_GET_ADDRESSES
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19c68a354e0ad3b040a2a0d4a2a4d761642f3303
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918232"
---
# <a name="oid_co_get_addresses"></a>OID_CO_GET_ADDRESSES

OID_CO_GET_ADDRESSES OID は、呼び出しマネージャーに対してクエリを実行するためにクライアントによって使用されます。 このクエリは、コールマネージャーがクライアントに OID_CO_ADDRESS_CHANGE を送信することに応答して作成されます。 このクエリに応答して、呼び出しマネージャーは、次のように定義された CO_ADDRESS_LIST 構造として書式設定されたアドレス一覧をクライアントに送信します。

```c++
typedef struct _CO_ADDRESS_LIST {
    ULONG       NumberOfAddressesAvailable;
    ULONG       NumberOfAddresses;
    CO_ADDRESS  AddressList;
} CO_ADDRESS_LIST, *PCO_ADDRESS_LIST;
```

この構造体のメンバーには、次の情報が含まれています。

**使用可能な Numberofアドレス**  
通話マネージャーのアドレスリスト内のアドレスの最大数を指定します。 呼び出しマネージャーが**addresslist**でクライアントに返すアドレスの実際の数に関係なく、 **addresslist**のバッファーのサイズは常に、呼び出しマネージャーに固有の固定サイズであるアドレスサイズを乗算した**numberofaddresses を使用でき**ます。

**NumberOfAddresses**  
呼び出しマネージャーが**AddressList**に書き込んだアドレスの数を指定します。

**AddressList**  
エイリアスアドレスは、次のように定義された CO_ADDRESS 構造として書式設定されます。

```c++
typedef struct _CO_ADDRESS {
    ULONG   AddressSize;
    UCHAR   Address[1];
} CO_ADDRESS, *PCO_ADDRESS;
```

この構造体のメンバーには、次の情報が含まれています。

**AddressSize**  
**アドレス**の構造体のサイズをバイト単位で指定します。

**アドレス**  
アドレスの一覧を含む可変長配列を指定します。 アドレスの形式は、コールマネージャーによって使用されるシグナリングプロトコルに固有です。

**AddressList**には、ローカルホストに到達できるネットワークアドレスが含まれています。 特定のクライアントに返される**AddressList**には、すべてのクライアントに共通のアドレスと、クライアント自体が OID_CO_ADD_ADDRESS でマネージャーのアドレス一覧に追加したアドレスが含まれます。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

