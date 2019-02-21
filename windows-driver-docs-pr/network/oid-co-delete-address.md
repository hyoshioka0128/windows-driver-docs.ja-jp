---
title: OID_CO_DELETE_ADDRESS
description: このトピックでは、OID_CO_DELETE_ADDRESS オブジェクト識別子 (OID) について説明します。
ms.assetid: 987c839b-f673-4c7a-90b4-fc5f93454b2e
keywords:
- OID_CO_DELETE_ADDRESS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 271061deee0f234432fe0de82fbc52a42c665736
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551093"
---
# <a name="oidcodeleteaddress"></a>OID_CO_DELETE_ADDRESS

OID_CO_DELETE_ADDRESS OID は、ホストのエイリアスのアドレスを削除する、クライアントが、コール マネージャーに送信されます。 エイリアスのアドレス形式は次のように定義されている CO_ADDRESS 構造体としてです。

```c++
typedef struct _CO_ADDRESS {
    ULONG   AddressSize;
    UCHAR   Address[1];
} CO_ADDRESS, *PCO_ADDRESS; 
```

この構造体のメンバーには、次の情報が含まれます。

**AddressSize**  
アドレスの構造のバイト単位のサイズを指定します。

**アドレス**  
エイリアスのアドレスを含む可変長配列を指定します。 アドレスの形式は、コール マネージャーによって使用される信号のプロトコルに固有です。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

