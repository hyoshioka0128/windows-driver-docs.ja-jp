---
title: OID_CO_ADD_ADDRESS
description: このトピックでは、OID_CO_ADD_ADDRESS オブジェクト識別子 (OID) について説明します。
ms.assetid: ca6bb3eb-87db-4e71-9585-34cd1e978b6a
keywords:
- OID_CO_ADD_ADDRESS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05a27322f98fc08570bfb2d17d51aa115c90852a
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916838"
---
# <a name="oid_co_add_address"></a>OID_CO_ADD_ADDRESS

OID_CO_ADD_ADDRESS OID は、ホストのエイリアスアドレスを指定するために、クライアントから呼び出しマネージャーに送信されます。 エイリアスアドレスは、次のように定義された CO_ADDRESS 構造として書式設定されます。

```c++
typedef struct _CO_ADDRESS{
    ULONG   AddressSize;
    UCHAR   Address[1];
} CO_ADDRESS, *PCO_ADDRESS;
```

この構造体のメンバーには、次の情報が含まれています。

**AddressSize**  
**アドレス**の構造体のサイズをバイト単位で指定します。

**アドレス**  
エイリアスアドレスを含む可変長配列を指定します。 アドレスの形式は、コールマネージャーによって使用されるシグナリングプロトコルに固有です。

通常、この OID は、ホストが特定のサービスを提供する既知のアドレスを指定するために使用されます。 たとえば、クライアントは、LAN エミュレーションサーバーの既知のアドレスを指定できます。 この OID に対する呼び出しマネージャーの応答は、コールマネージャーによって使用されるシグナリングプロトコルに固有のものです。 たとえば、ATM コールマネージャーは、エイリアスアドレスのスイッチを通知するメッセージをスイッチに送信します。


## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

