---
title: OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS
description: このトピックでは、OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS オブジェクト識別子 (OID) について説明します。
ms.assetid: a56affc9-4118-4322-85bc-f979b70e0dad
keywords:
- OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0dbdfaea474136031da514840cd4c5d167d2729
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824052"
---
# <a name="oid_co_tapi_translate_ndis_callparams"></a>OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS

OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS OID は、 [CO_CALL_PARAMETERS](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))構造体でクライアントの[ProtocolClIncomingCall](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_call)関数に渡される NDIS 呼び出しパラメーターを TAPI 呼び出しパラメーターに変換するように、呼び出しマネージャーまたは mcm ドライバーに要求します。 クライアントは、通話マネージャーまたは MCM ドライバーによって返された変換済みの TAPI 呼び出しパラメーターを使用して、着信呼び出しを受け入れるか拒否するかを決定します。

この要求では、次のように定義されている CO_TAPI_TRANSLATE_NDIS_CALLPARAMS 構造体を使用します。

```c++
typedef struct _CO_TAPI_TRANSLATE_NDIS_CALLPARAMS {
    IN  ULONG               ulFlags;
    IN  NDIS_VAR_DATA_DESC  NdisCallParams;
    OUT NDIS_VAR_DATA_DESC  LineCallInfo;
} CO_TAPI_TRANSLATE_NDIS_CALLPARAMS, *PCO_TAPI_TRANSLATE_NDIS_CALLPARAMS;
```

この構造体のメンバーには、次の情報が含まれています。

**ulFlags**  
クライアントは、 **Ulflags**に CO_TAPI_FLAG_INCOMING_CALL ビットを設定する必要があります。

**NdisCallParams**  
NDIS_VAR_DATA_DESC 構造体の先頭から[CO_CALL_PARAMETERS](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))構造体までのオフセットを格納する[NDIS_VAR_DATA_DESC](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559020(v=vs.85))構造体を指定します。 NDIS_VAR_DATA_DESC 構造体には、CO_CALL_PARAMETERS 構造体の長さも含まれます。 クライアントは、CO_CALL_PARAMETERS 構造体に NDIS 呼び出しパラメーターを入力して、TAPI 呼び出しパラメーターに変換します。

**LineCallInfo**  
NDIS_VAR_DATA_DESC 構造体の先頭から LINE_CALL_INFO 構造体までのオフセットを格納する[NDIS_VAR_DATA_DESC](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559020(v=vs.85))構造体を指定します。 NDIS_VAR_DATA_DESC 構造体には、CO_CALL_PARAMETERS 構造体の長さも含まれます。 LINE_CALL_INFO 構造体は、指定された NDIS 呼び出しパラメーターが変換された TAPI 呼び出しパラメーターを指定します。 LINE_CALL_INFO 構造体の詳細については、Windows SDK と ndistapi .h のヘッダーファイルを参照してください。

## <a name="remarks"></a>注釈

要求が成功した場合、呼び出しマネージャーまたは MCM ドライバーは、 **LineCallInfo**によって参照される LINE_CALL_PARAMS 構造体に、変換された TAPI 呼び出しパラメーターを入力します。 呼び出しマネージャーまたは MCM ドライバーは、 **LineCallInfo**と呼ばれるフラットメモリセクション内に LINE_CALL_INFO 構造体を割り当てる必要があります。 クライアントは、LINE_CALL_INFO 構造体の合計長を**LineCallInfo**に書き込みます。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis (Ndis .h を含む) |

