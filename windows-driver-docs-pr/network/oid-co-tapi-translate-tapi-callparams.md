---
title: OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS
description: このトピックでは、OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS オブジェクト識別子 (OID) について説明します。
ms.assetid: bee8871d-9166-4c5a-8428-964f8b321cf1
keywords:
- OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48009bed0a7d7f7a66e83ad3b3de62bafc768c60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380703"
---
# <a name="oidcotapitranslatetapicallparams"></a>OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS

OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS OID は、NDIS 呼び出しのパラメーターに TAPI 呼び出しのパラメーターを変換するには、コール マネージャーまたは統合呼び出し manager ミニポート (MCM) ドライバーを要求します。 この OID が返される NDIS を使用してクエリが入力としてパラメーターを呼び出すクライアント (として書式設定、 [CO_CALL_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff545384)構造) に[NdisClMakeCall](https://msdn.microsoft.com/library/windows/hardware/ff561635)クライアントが発信呼び出しを配置します。

この OID は、次のように定義されている CO_TAPI_TRANSLATE_TAPI_CALLPARAMS 構造体を使用します。

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

この構造体のメンバーには、次の情報が含まれます。

**ulLineID**  
発信通話の転送先の 0 から始まる行識別子を指定します。

**ulAddressID**  
0 から始まるアドレスの識別子を指定します (で指定された行に**ulLineID**) を発信呼び出しを送信します。

**ulFlags**  
クライアントは、ビット CO_TAPI_FLAG_OUTGOING_CALL を設定する必要があります**ulFlags**します。 クライアントがビット CO_TAPI_USE_DEFAULT_CALLPARAMS を必要に応じて設定**ulFlags**を無視するには、コール マネージャーまたは MCM のドライバーを必要とする、 **LineCallParams**戻り値の既定の NDIS 呼び出しパラメーターデバイスです。

**DestAddress**  
指定します、 [NDIS_VAR_DATA_DESC](https://msdn.microsoft.com/library/windows/hardware/ff559020) NDIS_VAR_DATA_DESC 構造体の先頭から宛先アドレスへのオフセットを含む構造体が文字配列として書式設定します。 NDIS_VAR_DATA_DESC 構造体には、宛先アドレスの長さも含まれています。 送信先アドレスは、発信通話の転送先アドレスです。

**LineCallParams**  
指定します、 [NDIS_VAR_DATA_DESC](https://msdn.microsoft.com/library/windows/hardware/ff559020) LINE_CALL_PARAMS 構造に NDIS_VAR_DATA_DESC 構造体の先頭からのオフセットを含む構造体。 NDIS_VAR_DATA_DESC 構造体には、LINE_CALL_PARAMS 構造体の長さも含まれています。 LINE_CALL_PARAMS 構造体には、NDIS 呼び出しのパラメーターに変換する TAPI 呼び出しのパラメーターを指定します。 LINE_CALL_PARAMS 構造の詳細については、Microsoft Windows SDK と ndistapi.h ヘッダー ファイルを参照してください。

**NdisCallParams**  
指定します、 [NDIS_VAR_DATA_DESC](https://msdn.microsoft.com/library/windows/hardware/ff559020) CO_CALL_PARAMETERS 構造に NDIS_VAR_DATA_DESC 構造体の先頭からのオフセットを含む構造体。 NDIS_VAR_DATA_DESC 構造がの長さにはも含まれています、 [CO_CALL_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff545384)構造体。 CO_CALL_PARAMETERS 構造体は、特定の TAPI 呼び出しのパラメーターに翻訳された NDIS 呼び出しのパラメーターを指定します。

## <a name="remarks"></a>注釈

によって参照される CO_CALL_PARAMETERS 構造でコール マネージャーまたは MCM ドライバーが入力要求が成功した場合、 **NdisCallParams**翻訳済みの NDIS と呼び出しのパラメーター。 コール マネージャーまたは MCM ドライバーによって参照されるフラットなメモリの範囲内で CO_CALL_PARAMETERS 構造体を割り当て**NdisCallParams**します。 CO_CALL_PARAMETERS 構造体の長さの合計は、クライアントが書き込む**NdisCallParams.Length**します。

場合は、クライアント設定内のビット CO_TAPI_USE_DEFAULT_CALLPARAMS **ulFlags**クライアントが TAPI 呼び出しのパラメーターを指定していません。 この場合、コール マネージャーまたは MCM ドライバーは、デバイスの既定の NDIS 呼び出しパラメーターを返す必要があります。 デバイスの既定の NDIS 呼び出しパラメーターがない場合、コール マネージャーまたは MCM ドライバーは NDIS_STATUS_FAILURE を返す必要があります。


## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

