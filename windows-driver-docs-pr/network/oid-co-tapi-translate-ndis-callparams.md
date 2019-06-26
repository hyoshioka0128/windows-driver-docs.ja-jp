---
title: OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS
description: このトピックでは、OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS オブジェクト識別子 (OID) について説明します。
ms.assetid: a56affc9-4118-4322-85bc-f979b70e0dad
keywords:
- OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e86a743e2328344a8194fb200c2753dc23773b1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385507"
---
# <a name="oidcotapitranslatendiscallparams"></a>OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS

OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS OID 要求 NDIS 呼び出しのパラメーターを変換するには、コール マネージャーまたは MCM ドライバー (渡された、 [CO_CALL_PARAMETERS](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))構造体をクライアントの[ProtocolClIncomingCall](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_incoming_call)関数) から TAPI には、呼び出しパラメーター。 クライアントでは、コール マネージャーまたは MCM ドライバーによって返される翻訳された TAPI 呼び出しパラメーターを使用して、受け入れるか、着信通話を拒否するかどうかを判断します。

この要求は、次のように定義されている CO_TAPI_TRANSLATE_NDIS_CALLPARAMS 構造体を使用します。

```c++
typedef struct _CO_TAPI_TRANSLATE_NDIS_CALLPARAMS {
    IN  ULONG               ulFlags;
    IN  NDIS_VAR_DATA_DESC  NdisCallParams;
    OUT NDIS_VAR_DATA_DESC  LineCallInfo;
} CO_TAPI_TRANSLATE_NDIS_CALLPARAMS, *PCO_TAPI_TRANSLATE_NDIS_CALLPARAMS;
```

この構造体のメンバーには、次の情報が含まれます。

**ulFlags**  
クライアントは、ビット CO_TAPI_FLAG_INCOMING_CALL を設定する必要があります**ulFlags**します。

**NdisCallParams**  
指定します、 [NDIS_VAR_DATA_DESC](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559020(v=vs.85)) NDIS_VAR_DATA_DESC 構造体の先頭からのオフセットを含む構造体、 [CO_CALL_PARAMETERS](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))構造体。 NDIS_VAR_DATA_DESC 構造体には、CO_CALL_PARAMETERS 構造体の長さも含まれています。 クライアントは、TAPI 呼び出しのパラメーターに変換する NDIS 呼び出しパラメーターを持つ CO_CALL_PARAMETERS 構造体に格納します。

**LineCallInfo**  
指定します、 [NDIS_VAR_DATA_DESC](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559020(v=vs.85)) LINE_CALL_INFO 構造に NDIS_VAR_DATA_DESC 構造体の先頭からのオフセットを含む構造体。 NDIS_VAR_DATA_DESC 構造体には、CO_CALL_PARAMETERS 構造体の長さも含まれています。 LINE_CALL_INFO 構造では、翻訳されたパラメーターを呼び出し、特定の NDIS 先 TAPI 呼び出しのパラメーターを指定します。 LINE_CALL_INFO 構造の詳細については、Windows SDK と ndistapi.h ヘッダー ファイルを参照してください。

## <a name="remarks"></a>注釈

によって参照される LINE_CALL_PARAMS 構造でコール マネージャーまたは MCM ドライバーが入力要求が成功した場合、 **LineCallInfo**翻訳 tapi 呼び出しパラメーター。 呼ばれるフラットなメモリの範囲内で LINE_CALL_INFO 構造を割り当てる必要があります、コール マネージャーまたは MCM ドライバー **LineCallInfo**します。 LINE_CALL_INFO 構造体の長さの合計は、クライアントが書き込む**LineCallInfo.Length**します。

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

