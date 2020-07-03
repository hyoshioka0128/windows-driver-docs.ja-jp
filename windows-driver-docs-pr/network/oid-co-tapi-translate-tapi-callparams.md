---
title: OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS
description: このトピックでは、OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS オブジェクト識別子 (OID) について説明します。
ms.assetid: bee8871d-9166-4c5a-8428-964f8b321cf1
keywords:
- OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8a6510c985220906d8fcc13e7cfa48feb483e9e
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917512"
---
# <a name="oid_co_tapi_translate_tapi_callparams"></a>OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS

OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS OID は、TAPI 呼び出しパラメーターを NDIS 呼び出しパラメーターに変換するために、呼び出しマネージャーまたは統合された call manager ミニポート (MCM) ドライバーを要求します。 この OID に対してクエリを行うクライアントは、返された NDIS 呼び出しパラメーターを[NdisClMakeCall](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmakecall)に入力 ( [CO_CALL_PARAMETERS](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))構造として書式設定) として使用し、クライアントが発信呼び出しを配置します。

この OID では、次のように定義されている CO_TAPI_TRANSLATE_TAPI_CALLPARAMS 構造体を使用します。

```c++
typedef struct _CO_TAPI_TRANSLATE_TAPI_CALLPARAMS {
    IN  ULONG               ulLineID;
    IN  ULONG               ulAddressID;
    IN  ULONG               ulFlags;
    IN  NDIS_VAR_DATA_DESC  DestAddress;
    IN  NDIS_VAR_DATA_DESC  LineCallParams;
    OUT NDIS_VAR_DATA_DESC  NdisCallParams;
} CO_TAPI_TRANSLATE_TAPI_CALLPARAMS, *PCO_TAPI_TRANSLATE_TAPI_CALLPARAMS;
```

この構造体のメンバーには、次の情報が含まれています。

**ulLineID**  
発信呼び出しの送信先となる、0から始まる行識別子を指定します。

**ulAddressID**  
発信呼び出しの送信先となる、0から始まるアドレス識別子を指定します ( **ulLineID**で指定された行)。

**ulFlags**  
クライアントは、 **Ulflags**に CO_TAPI_FLAG_OUTGOING_CALL ビットを設定する必要があります。 クライアントは必要に応じて、LineCallParams ビットを**Ulflags**に CO_TAPI_USE_DEFAULT_CALLPARAMS 設定して、呼び出しマネージャーまたは mcm ドライバーが**LineCallParams**を無視し、デバイスの既定の NDIS 呼び出しパラメーターを返すようにする必要があります。

**DestAddress**  
NDIS_VAR_DATA_DESC 構造体の先頭から、文字配列として書式設定された宛先アドレスへのオフセットを格納する[NDIS_VAR_DATA_DESC](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559020(v=vs.85))構造体を指定します。 NDIS_VAR_DATA_DESC 構造体には、宛先アドレスの長さも含まれます。 送信先アドレスは、発信呼び出しの送信先アドレスです。

**LineCallParams**  
NDIS_VAR_DATA_DESC 構造体の先頭から LINE_CALL_PARAMS 構造体までのオフセットを格納する[NDIS_VAR_DATA_DESC](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559020(v=vs.85))構造体を指定します。 NDIS_VAR_DATA_DESC 構造体には、LINE_CALL_PARAMS 構造体の長さも含まれます。 LINE_CALL_PARAMS 構造体は、NDIS 呼び出しパラメーターに変換される TAPI 呼び出しパラメーターを指定します。 LINE_CALL_PARAMS 構造体の詳細については、Microsoft Windows SDK と ndistapi .h ヘッダーファイルを参照してください。

**NdisCallParams**  
NDIS_VAR_DATA_DESC 構造体の先頭から CO_CALL_PARAMETERS 構造体までのオフセットを格納する[NDIS_VAR_DATA_DESC](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559020(v=vs.85))構造体を指定します。 NDIS_VAR_DATA_DESC 構造体には、 [CO_CALL_PARAMETERS](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))構造体の長さも含まれます。 CO_CALL_PARAMETERS 構造体は、指定された TAPI 呼び出しパラメーターが変換された NDIS 呼び出しパラメーターを指定します。

## <a name="remarks"></a>注釈

要求が成功した場合、呼び出しマネージャーまたは MCM ドライバーは、 **NdisCallParams**によって参照される構造体 CO_CALL_PARAMETERS に、変換された NDIS 呼び出しパラメーターを格納します。 呼び出しマネージャーまたは MCM ドライバーは、 **NdisCallParams**によって参照されるフラットメモリセクション内に CO_CALL_PARAMETERS 構造体を割り当てる必要があります。 クライアントは、CO_CALL_PARAMETERS 構造体の合計長を**NdisCallParams**に書き込みます。

クライアントが**Ulflags**に CO_TAPI_USE_DEFAULT_CALLPARAMS ビットを設定した場合、クライアントは TAPI 呼び出しパラメーターを指定しません。 この場合、呼び出しマネージャーまたは MCM ドライバーは、デバイスの既定の NDIS 呼び出しパラメーターを返す必要があります。 デバイスに既定の NDIS 呼び出しパラメーターがない場合、呼び出しマネージャーまたは MCM ドライバーは NDIS_STATUS_FAILURE を返す必要があります。


## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

