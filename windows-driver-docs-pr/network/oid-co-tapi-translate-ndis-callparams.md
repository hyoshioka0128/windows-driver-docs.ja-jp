---
title: OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS
description: このトピックでは、OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS オブジェクト識別子 (OID) について説明します。
ms.assetid: a56affc9-4118-4322-85bc-f979b70e0dad
keywords:
- OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9ced54e40c9f1a421a07b2f154cc7da31aecdb8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380704"
---
# <a name="oidcotapitranslatendiscallparams"></a>OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS

OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS OID 要求 NDIS 呼び出しのパラメーターを変換するには、コール マネージャーまたは MCM ドライバー (渡された、 [CO_CALL_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff545384)構造体をクライアントの[ProtocolClIncomingCall](https://msdn.microsoft.com/library/windows/hardware/ff570228)関数) から TAPI には、呼び出しパラメーター。 クライアントでは、コール マネージャーまたは MCM ドライバーによって返される翻訳された TAPI 呼び出しパラメーターを使用して、受け入れるか、着信通話を拒否するかどうかを判断します。

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
指定します、 [NDIS_VAR_DATA_DESC](https://msdn.microsoft.com/library/windows/hardware/ff559020) NDIS_VAR_DATA_DESC 構造体の先頭からのオフセットを含む構造体、 [CO_CALL_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff545384)構造体。 NDIS_VAR_DATA_DESC 構造体には、CO_CALL_PARAMETERS 構造体の長さも含まれています。 クライアントは、TAPI 呼び出しのパラメーターに変換する NDIS 呼び出しパラメーターを持つ CO_CALL_PARAMETERS 構造体に格納します。

**LineCallInfo**  
指定します、 [NDIS_VAR_DATA_DESC](https://msdn.microsoft.com/library/windows/hardware/ff559020) LINE_CALL_INFO 構造に NDIS_VAR_DATA_DESC 構造体の先頭からのオフセットを含む構造体。 NDIS_VAR_DATA_DESC 構造体には、CO_CALL_PARAMETERS 構造体の長さも含まれています。 LINE_CALL_INFO 構造では、翻訳されたパラメーターを呼び出し、特定の NDIS 先 TAPI 呼び出しのパラメーターを指定します。 LINE_CALL_INFO 構造の詳細については、Windows SDK と ndistapi.h ヘッダー ファイルを参照してください。

## <a name="remarks"></a>注釈

によって参照される LINE_CALL_PARAMS 構造でコール マネージャーまたは MCM ドライバーが入力要求が成功した場合、 **LineCallInfo**翻訳 tapi 呼び出しパラメーター。 呼ばれるフラットなメモリの範囲内で LINE_CALL_INFO 構造を割り当てる必要があります、コール マネージャーまたは MCM ドライバー **LineCallInfo**します。 LINE_CALL_INFO 構造体の長さの合計は、クライアントが書き込む**LineCallInfo.Length**します。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

