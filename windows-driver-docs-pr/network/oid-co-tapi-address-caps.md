---
title: OID_CO_TAPI_ADDRESS_CAPS
description: このトピックでは、OID_CO_TAPI_ADDRESS_CAPS オブジェクト識別子 (OID) について説明します。
ms.assetid: c0e44c1b-89d1-4c50-a1fc-8322bb1d00c2
keywords:
- OID_CO_TAPI_ADDRESS_CAPS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 136a7b1a892e817cff0c6acd1a5a13fd01624c87
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380712"
---
# <a name="oidcotapiaddresscaps"></a>OID_CO_TAPI_ADDRESS_CAPS

OID_CO_TAPI_ADDRESS_CAPS OID を特定の行で指定されたアドレスのテレフォニー機能を返すには、コール マネージャーまたは統合ミニポート コール マネージャー (MCM) ドライバーを要求します。

この要求は、次のように定義されている CO_TAPI_ADDRESS_CAPS 構造体を使用します。

```c++
typedef struct _CO_TAPI_ADDRESS_CAPS {
    IN  ULONG               ulLineID;
    IN  ULONG               ulAddressID;
    OUT ULONG               ulFlags;
    OUT LINE_ADDRESS_CAPS   LineAddressCaps;
} CO_TAPI_ADDRESS_CAPS, *PCO_TAPI_ADDRESS_CAPS;
``` 

この構造体のメンバーには、次の情報が含まれます。

**ulLineID**  
指定されたアドレスが配置されている行の 0 から始まる行識別子を指定します。

**ulAddressID**  
機能が返される行の 0 から始まるアドレスの識別子を指定します。

**ulFlags**  
これらのフラグが予約されています。

**LineAddressCaps**  
LINE_ADDRESS_CAPS 構造として書式設定された、アドレスのテレフォニー機能を指定します。 この構造体の詳細については、Microsoft Windows SDK と ndistapi.h ヘッダー ファイルを参照してください。

## <a name="remarks"></a>注釈

コール マネージャーのまたは MCM ドライバーのデバイスの行の機能を照会した[OID_CO_TAPI_LINE_CAPS](oid-co-tapi-line-caps.md)、接続指向のクライアントは、各行のアドレスの機能を次のようにクエリします。

- クライアントはすべての機能を決定する OID_CO_TAPI_ADDRESS_CAPS 1 回照会 OID_CO_TAPI_LINE_CAPS の前のクエリに行が 1 つのアドレスをサポートするか、行のすべてのアドレスが同じアドレス機能を備えている、指定した場合、行のアドレス。 この場合、コール マネージャーによって返されるアドレス機能または MCM ドライバーは、行のすべてのアドレスに適用されます。

- 行は、複数の異なる機能を備えた複数のアドレスをサポートする場合、クライアントにクエリを OID_CO_TAPI_ADDRESS_CAPS 1 回、行の各アドレス。 この場合、コール マネージャーによって返されるアドレス機能または MCM のドライバーが特定の行で指定されたアドレスに適用されます。

指定されたアドレスのアドレスの機能を返します、コール マネージャーまたは MCM ドライバー **LineAddressCaps**します。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

