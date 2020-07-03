---
title: OID_CO_TAPI_CM_CAPS
description: このトピックでは、OID_CO_TAPI_CM_CAPS オブジェクト識別子 (OID) について説明します。
ms.assetid: c0e44c1b-89d1-4c50-a1fc-8322bb1d00c2
keywords:
- OID_CO_TAPI_CM_CAPS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3260327315567fdab76d57767d2a6247761c3ac
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917532"
---
# <a name="oid_co_tapi_cm_caps"></a>OID_CO_TAPI_CM_CAPS

OID_CO_TAPI_CM_CAPS OID は、コールマネージャーまたは統合されたミニポート呼び出しマネージャー (MCM) ドライバーに対して、デバイス (呼び出し管理サービスを提供するデバイス) によってサポートされる行の数を返すように要求します。 また、この OID は呼び出しマネージャーまたは MCM ドライバーに対して、行の機能が異なるかどうかを示すように要求します。

この要求では、次のように定義されている CO_TAPI_CM_CAPS 構造を使用します。

```c++
typedef struct _CO_TAPI_CM_CAPS {
    OUT ULONG   ulCoTapiVersion;
    OUT ULONG   ulNumLines;
    OUT ULONG   ulFlags;
} CO_TAPI_CM_CAPS, *PCO_TAPI_CM_CAPS;
``` 

この構造体のメンバーには、次の情報が含まれています。

**ulCoTapiVersion**  
通話マネージャーまたは MCM ドライバーでサポートされている TAPI バージョンを指定します。 呼び出しマネージャーまたは MCM ドライバーは、これを CO_TAPI_VERSION に設定する必要があります。

**ulNumLines**  
デバイスでサポートされる行の数を指定します。

**ulFlags**  
デバイスで回線機能が異なる複数の行がサポートされている場合、またはこれらの行のアドレスのアドレスが異なる場合、呼び出しマネージャーまたは MCM ドライバーは、 **Ulflags**に CO_TAPI_FLAG_PER_LINE_CAPS ビットを設定します。それ以外の場合、呼び出しマネージャーまたは MCM ドライバーはこのビットをクリアします。 未定義のビットは、将来使用するために予約されており、0に設定する必要があります。

## <a name="remarks"></a>注釈

接続指向クライアントは、この OID から返された情報を使用して、呼び出しマネージャーまたは MCM ドライバーのデバイスのライン機能を[OID_CO_TAPI_LINE_CAPS](oid-co-tapi-line-caps.md)で照会する方法を決定します。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

