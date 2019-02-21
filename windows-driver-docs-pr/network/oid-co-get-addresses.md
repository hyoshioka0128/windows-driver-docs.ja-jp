---
title: OID_CO_GET_ADDRESSES
description: このトピックでは、OID_CO_GET_ADDRESSES オブジェクト識別子 (OID) について説明します。
ms.assetid: 0c30e184-be01-49ab-b9ad-3ccc2fdf9fc5
keywords:
- OID_CO_GET_ADDRESSES
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9004aadc69b1a2d2afa3d9b1ab426cc77df8adb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531690"
---
# <a name="oidcogetaddresses"></a>OID_CO_GET_ADDRESSES

OID_CO_GET_ADDRESSES OID は、コール マネージャーにクエリをクライアントによって使用されます。 このクエリは、OID_CO_ADDRESS_CHANGE をクライアントに送信呼び出しのマネージャーへの応答で作成されます。 このクエリに応答してでコール マネージャーをクライアントに送信アドレス一覧書式設定されている次のように定義されている CO_ADDRESS_LIST 構造体として。

```c++
typedef struct _CO_ADDRESS_LIST {
    ULONG       NumberOfAddressesAvailable;
    ULONG       NumberOfAddresses;
    CO_ADDRESS  AddressList;
} CO_ADDRESS_LIST, *PCO_ADDRESS_LIST;
```

この構造体のメンバーには、次の情報が含まれます。

**NumberOfAddressesAvailable**  
アドレスのコール マネージャーの一覧で、アドレスの最大数を指定します。 クライアントにコール マネージャーが返すアドレスの実際の数に関係なく**AddressList**、バッファーのサイズ**AddressList**は常に**NumberOfAddressesAvailable**コール マネージャーに固有の固定サイズであるアドレスのサイズを乗算します。

**NumberOfAddresses**  
コール マネージャーに書き込まれるアドレスの数を指定します**AddressList**します。

**AddressList**  
エイリアスのアドレス形式は次のように定義されている CO_ADDRESS 構造体としてです。

```c++
typedef struct _CO_ADDRESS {
    ULONG   AddressSize;
    UCHAR   Address[1];
} CO_ADDRESS, *PCO_ADDRESS;
```

この構造体のメンバーには、次の情報が含まれます。

**AddressSize**  
構造のバイト単位のサイズを指定します。**アドレス**します。

**アドレス**  
アドレスの一覧を含む可変長配列を指定します。 アドレスの形式は、コール マネージャーによって使用される信号のプロトコルに固有です。

**AddressList**ローカル ホストに到達できるネットワーク アドレスが含まれます。 **AddressList**特定に返されるクライアントには、クライアント自体が OID_CO_ADD_ADDRESS とアドレスのコール マネージャーの一覧に追加するすべてのアドレスと同様に、すべてのクライアントに共通するアドレスが含まれています。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

