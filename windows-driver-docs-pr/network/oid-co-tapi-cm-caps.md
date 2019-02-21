---
title: OID_CO_TAPI_CM_CAPS
description: このトピックでは、OID_CO_TAPI_CM_CAPS オブジェクト識別子 (OID) について説明します。
ms.assetid: c0e44c1b-89d1-4c50-a1fc-8322bb1d00c2
keywords:
- OID_CO_TAPI_CM_CAPS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc20e53411e46cf75a3e86d44b7f63a4d1f4c24f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549527"
---
# <a name="oidcotapicmcaps"></a>OID_CO_TAPI_CM_CAPS

OID_CO_TAPI_CM_CAPS OID 要求をそのデバイスでサポートされている行の数を返すには、コール マネージャーまたは統合ミニポート コール マネージャー (MCM) ドライバー (デバイスの管理サービスの呼び出しを提供する)。 この OID は、次の行に複数の異なる行の機能があるかどうかを示すには、コール マネージャーまたは MCM ドライバーも要求します。

この要求は、次のように定義されている CO_TAPI_CM_CAPS 構造体を使用します。

```c++
typedef struct _CO_TAPI_CM_CAPS {
    OUT ULONG   ulCoTapiVersion;
    OUT ULONG   ulNumLines;
    OUT ULONG   ulFlags;
} CO_TAPI_CM_CAPS, *PCO_TAPI_CM_CAPS;
``` 

この構造体のメンバーには、次の情報が含まれます。

**ulCoTapiVersion**  
コール マネージャーまたは MCM ドライバーによってサポートされている TAPI バージョンを指定します。 コール マネージャーまたは MCM ドライバー設定この CO_TAPI_VERSION します。

**ulNumLines**  
デバイスでサポートされている行の数を指定します。

**ulFlags**  
デバイスが複数の異なる行の機能を備えた複数の行をサポートまたはコール マネージャーまたは MCM のドライバーがビット CO_TAPI_FLAG_PER_LINE_CAPS を設定する場合、これらの行のいずれかのアドレスでは、アドレスの種類の異なる機能があります、 **ulFlags**;それ以外の場合、コール マネージャーまたは MCM ドライバーには、このビットがクリアします。 未定義のすべてのビットは将来使用するために予約されていると、0 に設定する必要があります。

## <a name="remarks"></a>注釈

接続指向のクライアントでは、この OID から返される情報を使用して、コール マネージャーのまたは MCM ドライバーのデバイスの行の機能をクエリする方法を決定[OID_CO_TAPI_LINE_CAPS](oid-co-tapi-line-caps.md)します。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

