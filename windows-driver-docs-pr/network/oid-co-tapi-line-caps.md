---
title: OID_CO_TAPI_LINE_CAPS
description: このトピックでは、OID_CO_TAPI_LINE_CAPS オブジェクト識別子 (OID) について説明します。
ms.assetid: 82c2bcb4-fb58-4e14-b1d4-2bcc0c4fcd1d
keywords:
- OID_CO_TAPI_LINE_CAPS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: c55b4c15b07c41afa7fe7f05b979cb921aad7e94
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551102"
---
# <a name="oidcotapilinecaps"></a>OID_CO_TAPI_LINE_CAPS

OID_CO_TAPI_LINE_CAPS OID は、指定した行のテレフォニー機能を返すには、コール マネージャーまたは統合ミニポート コール マネージャー (MCM) ドライバーを要求します。 この OID は、この行のアドレスが異種のテレフォニー機能を持つかどうかを示すには、コール マネージャーまたは MCM ドライバーにも要求します。

この要求は、特定の行のテレフォニー機能を照会する次のように定義されている、CO_TAPI_LINE_CAPS 構造体を使用します。

```c++
typedef struct _CO_TAPI_LINE_CAPS {
    IN  ULONG           ulLineID;
    OUT ULONG           ulFlags;
    OUT LINE_DEV_CAPS   LineDevCaps;
} CO_TAPI_LINE_CAPS, *PCO_TAPI_LINE_CAPS;
``` 

この構造体のメンバーには、次の情報が含まれます。

**ulLineID**  
どのテレフォニー機能が返される行を指定します。 **ulLineID**は 0 から始まる識別子です。

**ulFlags**  
行は、異種のテレフォニー機能を備えた複数のアドレスをサポートする場合、コール マネージャーまたは MCM ドライバー設定 ulFlags; 内のビット CO_TAPI_FLAG_PER_ADDRESS_CAPSそれ以外の場合、コール マネージャーまたは MCM ドライバーには、このビットがクリアします。 未定義のすべてのビットは予約されており、0 に設定する必要があります。

**LineDevCaps**  
LINE_DEV_CAPS 構造として書式設定された行のテレフォニー機能を指定します。 この構造体の詳細については、Microsoft Windows SDK と ndistapi.h ヘッダー ファイルを参照してください。

## <a name="remarks"></a>注釈

コール マネージャーのまたは MCM ドライバーのデバイスのテレフォニー機能を照会した[OID_CO_TAPI_CM_CAPS](oid-co-tapi-cm-caps.md)、接続指向のクライアントがデバイスでサポートされている行のテレフォニー機能を照会します。

- デバイスでサポートされているすべての行が行と同じ機能を持っており、これらの行のすべてのアドレスが同じアドレス機能を備えて、クライアントは、デバイスの行の機能を取得する OID_CO_TAPI_LINE_CAPS 1 回を照会します。 この場合、コール マネージャーによって返される行の機能または MCM のドライバーがデバイスでサポートされているすべての行に適用されます。
- 機能を取得するデバイスでサポートされている行ごとにただし、デバイスに複数の異なる機能を備えた複数の行がサポートしている場合、またはこれらの行のアドレスは、アドレスの種類の異なる機能を持つ場合は、クライアントが OID_CO_TAPI_LINE_CAPS を 1 回クエリします。各の行。

**UlFlags**設定は、クライアントは、その後、行のアドレスの機能を照会する回数を決定します。

- 行が 1 つのアドレスをサポートしている場合、または行が同じアドレス機能を備えた複数のアドレスをサポートしている場合、クライアントが 1 回 OID_CO_TAPI_ADDRESS_CAPS を照会します。
- 行は、複数の異なる機能を備えた複数のアドレスをサポートする場合、クライアント クエリ OID_CO_TAPI_ADDRESS_CAPS 1 回行には、各アドレスのください。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

