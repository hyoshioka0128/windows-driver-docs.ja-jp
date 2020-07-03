---
title: OID_CO_DELETE_ADDRESS
description: このトピックでは、OID_CO_DELETE_ADDRESS オブジェクト識別子 (OID) について説明します。
ms.assetid: 987c839b-f673-4c7a-90b4-fc5f93454b2e
keywords:
- OID_CO_DELETE_ADDRESS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: aad1289b726a2de12f058994df04f6d0311e50c3
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918204"
---
# <a name="oid_co_delete_address"></a>OID_CO_DELETE_ADDRESS

OID_CO_DELETE_ADDRESS OID は、ホストのエイリアスアドレスを削除するために、クライアントから呼び出しマネージャーに送信されます。 エイリアスアドレスは、次のように定義された CO_ADDRESS 構造として書式設定されます。

```c++
typedef struct _CO_ADDRESS {
    ULONG   AddressSize;
    UCHAR   Address[1];
} CO_ADDRESS, *PCO_ADDRESS; 
```

この構造体のメンバーには、次の情報が含まれています。

**AddressSize**  
アドレスの構造体のサイズをバイト単位で指定します。

**アドレス**  
エイリアスアドレスを含む可変長配列を指定します。 アドレスの形式は、コールマネージャーによって使用されるシグナリングプロトコルに固有です。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

