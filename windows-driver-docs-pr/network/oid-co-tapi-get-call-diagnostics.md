---
title: OID_CO_TAPI_GET_CALL_DIAGNOSTICS
description: このトピックでは、OID_CO_TAPI_GET_CALL_DIAGNOSTICS オブジェクト識別子 (OID) について説明します。
ms.assetid: 5b0b1a96-9d66-4ee3-9b9a-3341ca3a4b5c
keywords:
- OID_CO_TAPI_GET_CALL_DIAGNOSTICS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9a2aba33822e587782642eb0e58308b57c1d1f9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383259"
---
# <a name="oidcotapigetcalldiagnostics"></a>OID_CO_TAPI_GET_CALL_DIAGNOSTICS

OID_CO_TAPI_GET_CALL_DIAGNOSTICS OID は、失敗した呼び出しまたはリモートの TAPI パーティによって破棄呼び出しに関する診断情報を返すには、コール マネージャーまたは MCM のドライバーを要求します。

この要求は、次のように定義されている CO_TAPI_CALL_DIAGNOSTICS 構造体を使用します。

```c++
typedef struct _CO_TAPI_CALL_DIAGNOSTICS {
    OUT ULONG               ulOrigin;
    OUT ULONG               ulReason;
    OUT NDIS_VAR_DATA_DESC  DiagInfo;
} CO_TAPI_CALL_DIAGNOSTICS, *PCO_TAPI_CALL_DIAGNOSTICS;
```

**ulOrigin**  
LINECALLORIGIN_ 定数は、次の 1 つとして、呼び出しの発信元を指定します。 

- **LINECALLORIGIN_OUTBOUND**  
呼び出しは、発信呼び出しです。

- **LINECALLORIGIN_INTERNAL**  
呼び出しは、受信および内部で (たとえば同じ PBX) で発行されたです。

- **LINECALLORIGIN_EXTERNAL**呼び出しが着信し、発行された外部でします。

- **LINECALLORIGIN_UNKNOWN**  
呼び出しでは、受信されます。 原点は、現在既知ではありませんが、後で知られる可能性があります。

- **LINECALLORIGIN_UNAVAIL**  
呼び出しでは、受信されます。 原点は、ご利用いただけません、呼ばれることはありません。

- **LINECALLORIGIN_CONFERENCE**  
呼び出しハンドルは--電話会議は、スイッチで会議ブリッジへのアプリケーションの接続です。

**ulReason**  
LINECALLREASON_ 定数は、次の 1 つとして、呼び出しの理由を指定します。 

- **LINECALLREASON_DIRECT**  
呼び出しは、直接です。

- **LINECALLREASON_FWDBUSY**  
ビジー状態の拡張機能からの呼び出しが転送されました。

- **LINECALLREASON_FWDNOANSWER**  
未回答の拡張機能からいくつかのリングの後に、呼び出しが転送されました。

- **LINECALLREASON_FWDUNCOND**  
呼び出しは、別の数値から無条件で転送されました。

- **LINECALLREASON_PICKUP**  
呼び出しは、別の拡張機能から取得されました。

- **LINECALLREASON_UNPARK**  
保留中ルーティングの呼び出しと呼び出しが取得されました。

- **LINECALLREASON_REDIRECT**  
呼び出しは、このステーションにリダイレクトされました。

- **LINECALLREASON_CALLCOMPLETION**  
呼び出しでは、呼び出しの完了要求の結果はでした。

- **LINECALLREASON_TRANSFER**  
別の番号からの呼び出しが転送されました。 パーティの識別子情報がある可能性があります、呼び出し元であると、通話が転送します。

- **LINECALLREASON_REMINDER**  
呼び出しはアラーム (または「取り消し」) をユーザーが保留されている呼び出しを持つか、可能性のある長時間保留中します。

- **LINECALLREASON_UNKNOWN**  
呼び出しの理由は、現在既知ではありませんが、後で知られる可能性があります。

- **LINECALLREASON_UNAVAIL**  
呼び出しの理由では、ご利用いただけません、後で知られることはできません。

**DiagInfo**  
指定します、 [NDIS_VAR_DATA_DESC](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559020(v=vs.85))コール マネージャーまたは MCM ドライバーによって提供されるオプションの診断情報の長さとする、オフセットを含む構造体。 コンテンツと形式の診断情報は、ドライバーが決定します。

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

