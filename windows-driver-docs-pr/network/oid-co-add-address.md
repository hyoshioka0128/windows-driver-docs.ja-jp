---
title: OID_CO_ADD_ADDRESS
description: このトピックでは、OID_CO_ADD_ADDRESS オブジェクト識別子 (OID) について説明します。
ms.assetid: ca6bb3eb-87db-4e71-9585-34cd1e978b6a
keywords:
- OID_CO_ADD_ADDRESS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2969e6314ebd2fb24b0ce09104070069811476cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574326"
---
# <a name="oidcoaddaddress"></a>OID_CO_ADD_ADDRESS

OID_CO_ADD_ADDRESS OID は、ホストのエイリアスのアドレスを指定する、クライアントが、コール マネージャーに送信されます。 エイリアスのアドレス形式は次のように定義されている CO_ADDRESS 構造体としてです。

```c++
typedef struct _CO_ADDRESS{
    ULONG   AddressSize;
    UCHAR   Address[1];
} CO_ADDRESS, *PCO_ADDRESS;
```

この構造体のメンバーには、次の情報が含まれます。

**AddressSize**  
構造のバイト単位のサイズを指定します。**アドレス**します。

**アドレス**  
エイリアスのアドレスを含む可変長配列を指定します。 アドレスの形式は、コール マネージャーによって使用される信号のプロトコルに固有です。

この OID は通常ホストが特定のサービスを提供する、よく知られているアドレスを指定するために使用します。 たとえば、クライアントは、LAN エミュレーションのサーバーの既知のアドレスを指定できます。 この oid コール マネージャーの応答は、コール マネージャーによって使用される信号のプロトコルに固有です。 ATM コール マネージャーは、たとえば、エイリアスのアドレスのスイッチに通知するスイッチにメッセージを送信します。


## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

