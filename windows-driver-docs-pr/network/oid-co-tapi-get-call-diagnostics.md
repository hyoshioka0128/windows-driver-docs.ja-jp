---
title: OID_CO_TAPI_GET_CALL_DIAGNOSTICS
description: このトピックでは、OID_CO_TAPI_GET_CALL_DIAGNOSTICS オブジェクト識別子 (OID) について説明します。
ms.assetid: 5b0b1a96-9d66-4ee3-9b9a-3341ca3a4b5c
keywords:
- OID_CO_TAPI_GET_CALL_DIAGNOSTICS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 984bda7c7eace1c0999eab3b34a8dff241b9ec16
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917529"
---
# <a name="oid_co_tapi_get_call_diagnostics"></a>OID_CO_TAPI_GET_CALL_DIAGNOSTICS

OID_CO_TAPI_GET_CALL_DIAGNOSTICS OID は、呼び出しマネージャーまたは MCM ドライバーに対して、失敗した呼び出しまたはリモート TAPI パーティによって破棄された呼び出しに関する診断情報を返すように要求します。

この要求では、次のように定義されている CO_TAPI_CALL_DIAGNOSTICS 構造を使用します。

```c++
typedef struct _CO_TAPI_CALL_DIAGNOSTICS {
    OUT ULONG               ulOrigin;
    OUT ULONG               ulReason;
    OUT NDIS_VAR_DATA_DESC  DiagInfo;
} CO_TAPI_CALL_DIAGNOSTICS, *PCO_TAPI_CALL_DIAGNOSTICS;
```

**ulOrigin**  
呼び出しの発信先を、次のいずれかの LINECALLORIGIN_ 定数として指定します。 

- **LINECALLORIGIN_OUTBOUND**  
呼び出しは発信呼び出しです。

- **LINECALLORIGIN_INTERNAL**  
この呼び出しは受信され、内部的に発生します (たとえば、同じ PBX で)。

- **LINECALLORIGIN_EXTERNAL**呼び出しは受信され、外部から発信されます。

- **LINECALLORIGIN_UNKNOWN**  
呼び出しは着信です。 その配信元は現在不明ですが、後で認識される可能性があります。

- **LINECALLORIGIN_UNAVAIL**  
呼び出しは着信です。 そのオリジンは使用できず、知られることもありません。

- **LINECALLORIGIN_CONFERENCE**  
呼び出しハンドルは、会議呼び出し (つまり、アプリケーションからスイッチ内のカンファレンスブリッジへの接続) を対象としています。

**ulReason**  
呼び出しの理由を、次のいずれかの LINECALLREASON_ 定数として指定します。 

- **LINECALLREASON_DIRECT**  
呼び出しは直接です。

- **LINECALLREASON_FWDBUSY**  
呼び出しは、ビジー状態の拡張から転送されました。

- **LINECALLREASON_FWDNOANSWER**  
この呼び出しは、未回答の拡張機能からいくつかのリングの後に転送されました。

- **LINECALLREASON_FWDUNCOND**  
呼び出しは別の数値から無条件に転送されました。

- **LINECALLREASON_PICKUP**  
この呼び出しは別の拡張機能から取得されました。

- **LINECALLREASON_UNPARK**  
呼び出しは、保留中の呼び出しとして取得されました。

- **LINECALLREASON_REDIRECT**  
呼び出しがこのステーションにリダイレクトされました。

- **LINECALLREASON_CALLCOMPLETION**  
呼び出し完了要求の結果でした。

- **LINECALLREASON_TRANSFER**  
呼び出しは別の数値から転送されました。 パーティ id 情報は、呼び出し元がだれであるか、および呼び出しが転送された場所を示している場合があります。

- **LINECALLREASON_REMINDER**  
この呼び出しは、ユーザーが通話を保留しているか、長時間に及ぶ可能性のあるリマインダー ("リコール") です。

- **LINECALLREASON_UNKNOWN**  
この呼び出しの理由は、現在不明ですが、後で認識される可能性があります。

- **LINECALLREASON_UNAVAIL**  
この呼び出しの理由は使用できず、後で知ることはできません。

**DiagInfo**  
へのオフセット、および呼び出しマネージャーまたは MCM ドライバーによって提供されるオプションの診断情報の長さを含む[NDIS_VAR_DATA_DESC](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559020(v=vs.85))構造体を指定します。 診断情報の内容と形式は、ドライバーによって決まります。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

