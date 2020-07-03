---
title: OID_CO_TAPI_ADDRESS_CAPS
description: このトピックでは、OID_CO_TAPI_ADDRESS_CAPS オブジェクト識別子 (OID) について説明します。
ms.assetid: c0e44c1b-89d1-4c50-a1fc-8322bb1d00c2
keywords:
- OID_CO_TAPI_ADDRESS_CAPS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38825b1c6bb8e5e95e48a332dc68c5c71ae94e31
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916804"
---
# <a name="oid_co_tapi_address_caps"></a>OID_CO_TAPI_ADDRESS_CAPS

OID_CO_TAPI_ADDRESS_CAPS OID は、指定された行の指定されたアドレスのテレフォニー機能を返すために、呼び出しマネージャーまたは integrated ミニポート呼び出しマネージャー (MCM) ドライバーを要求します。

この要求では、次のように定義されている CO_TAPI_ADDRESS_CAPS 構造を使用します。

```c++
typedef struct _CO_TAPI_ADDRESS_CAPS {
    IN  ULONG               ulLineID;
    IN  ULONG               ulAddressID;
    OUT ULONG               ulFlags;
    OUT LINE_ADDRESS_CAPS   LineAddressCaps;
} CO_TAPI_ADDRESS_CAPS, *PCO_TAPI_ADDRESS_CAPS;
``` 

この構造体のメンバーには、次の情報が含まれています。

**ulLineID**  
指定したアドレスが配置されている行の0から始まる行識別子を指定します。

**ulAddressID**  
機能を返す行の0から始まるアドレス識別子を指定します。

**ulFlags**  
これらのフラグは予約されています。

**LineAddressCaps**  
LINE_ADDRESS_CAPS 構造として書式設定された、アドレスのテレフォニー機能を指定します。 この構造体の詳細については、Microsoft Windows SDK と ndistapi .h のヘッダーファイルを参照してください。

## <a name="remarks"></a>注釈

[OID_CO_TAPI_LINE_CAPS](oid-co-tapi-line-caps.md)を使用して call manager または mcm ドライバーのデバイスの回線機能に対してクエリを実行すると、接続指向クライアントは次のように、各行のアドレスの機能に対してクエリを実行します。

- OID_CO_TAPI_LINE_CAPS の前のクエリで、回線が1つのアドレスだけをサポートしていること、または行のすべてのアドレスが同じアドレス機能を持つことが示された場合、クライアントは、行のすべてのアドレスの機能を確認するために1回 OID_CO_TAPI_ADDRESS_CAPS をクエリします。 この場合、呼び出しマネージャーまたは MCM ドライバーによって返されるアドレス機能は、行のすべてのアドレスに適用されます。

- 機能が異なる複数のアドレスが回線でサポートされている場合、クライアントは行の各アドレスに対して1回ずつ OID_CO_TAPI_ADDRESS_CAPS クエリを実行します。 この場合、呼び出しマネージャーまたは MCM ドライバーによって返されるアドレス機能は、指定された行の指定したアドレスに適用されます。

呼び出しマネージャーまたは MCM ドライバーは、 **Lineaddresscaps**内の指定されたアドレスのアドレス機能を返します。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

