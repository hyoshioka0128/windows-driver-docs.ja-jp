---
title: OID_CO_TAPI_TRANSLATE_TAPI_SAP
description: このトピックでは、OID_CO_TAPI_TRANSLATE_TAPI_SAP オブジェクト識別子 (OID) について説明します。
ms.assetid: 701a1d02-8528-4b61-adbb-97c817194ac7
keywords:
- OID_CO_TAPI_TRANSLATE_TAPI_SAP
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: b15fd2a12a55088c3667d1dbbc6edca93e6748e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380701"
---
# <a name="oidcotapitranslatetapisap"></a>OID_CO_TAPI_TRANSLATE_TAPI_SAP

OID_CO_TAPI_TRANSLATE_TAPI_SAP OID は、TAPI の呼び出しのパラメーターから 1 つまたは複数の SAPs を準備するには、コール マネージャーまたは MCM の統合のドライバーを要求します。 この OID のクエリを実行するクライアントは、コール マネージャーまたは入力としての MCM ドライバーによって返される NDIS SAP を使用して (として書式設定、 [CO_SAP](https://msdn.microsoft.com/library/windows/hardware/ff545392)構造) に[NdisClRegisterSap](https://msdn.microsoft.com/library/windows/hardware/ff561648)で SAP を登録するクライアントを呼び出す着信呼び出しを受信します。

この要求は、次のように定義されている CO_TAPI_TRANSLATE_SAP 構造体を使用します。

```c++
typedef struct _CO_TAPI_TRANSLATE_SAP {
    IN  ULONG               ulLineID;
    IN  ULONG               ulAddressID;
    IN  ULONG               ulMediaModes;
    IN  ULONG               Reserved;
    OUT ULONG               NumberOfSaps;
    OUT NDIS_VAR_DATA_DESC  NdisSapParams[1];
} CO_AF_TAPI_SAP, *PCO_AF_TAPI_SAP;
```

この構造体のメンバーには、次の情報が含まれます。

**ulLineID**  
0 から始まる行識別子を指定します。

**ulAddressID**  
指定された行の 0 から始まるアドレスの識別子を指定**ulLineID**します。

**ulMediaModes**  
クライアントは、1 つ以上の次の LINEMEDIAMODE_constants としてでは、関心が呼び出しの情報ストリームのメディア モードを指定します。 

- **LINEMEDIAMODE_UNKNOWN**  
メディア ストリームが存在しますが、そのモードは、現在既知でないし、後で知られる可能性があります。 これは、未分類のメディアの種類、呼び出しに対応します。 一般的なアナログ テレフォニー環境での着信通話をメディア モードできない可能性がありますまで既知の呼び出しの回答し、を決定するフィルター選択されたメディア ストリーム。 

    場合、 **LINEMEDIAMODE_UNKNOWN**フラグが設定されて、その他のメディアのフラグを設定することもできます。 これは、メディアが不明であるが、その他の指定されたメディア モードのいずれかである可能性があることを示します。

- **LINEMEDIAMODE_INTERACTIVEVOICE**  
音声のエネルギーの呼び出しと呼び出しの有無は、両方の end の人間との対話型の呼び出しとして扱われます。

- **LINEMEDIAMODE_AUTOMATEDVOICE**  
音声のエネルギーの呼び出しと、音声の存在は、自動化されたアプリケーションによってローカル処理されます。

- **LINEMEDIAMODE_DATAMODEM**  
呼び出しでデータのモデム セッション。

- **LINEMEDIAMODE_G3FAX**  
グループ 3 の fax 送信または呼び出し経由で受信します。

- **LINEMEDIAMODE_G4FAX**  
グループ 4 の fax 送信または呼び出し経由で受信します。

- **LINEMEDIAMODE_TDD**  
呼び出しでの TDD (電気通信デバイス、聴覚が不自由) セッションです。

- **LINEMEDIAMODE_DIGITALDATA**  
デジタル データの送信または呼び出し経由で受信します。

- **LINEMEDIAMODE_TELETEX**  
呼び出しで teletex セッションです。 (Teletex はテレマティック サービスのいずれか) です。

- **LINEMEDIAMODE_VIDEOTEX**  
呼び出しで videotex セッションです。 (Videotex テレマティック サービスは、1 つです)。

- **LINEMEDIAMODE_TELEX**  
呼び出しでテレックス セッションです。 (テレックスはテレマティック サービスのいずれか) です。

- **LINEMEDIAMODE_MIXED**  
呼び出しに混在セッションです。 (混在、ISDN テレマティック サービスのいずれか)。

- **LINEMEDIAMODE_ADSI**  
呼び出しでの ADSI (アナログ ディスプレイ サービス インターフェイス) セッションです。

- **LINEMEDIAMODE_VOICEVIEW**  
呼び出しのメディア モードでは、VoiceView です。

**Reserved**  
これは予約されています。 クライアントは、このフィールドを 0 に設定する必要があります。

**NumberOfSaps**  
数を指定[NDIS_VAR_DATA_DESC](https://msdn.microsoft.com/library/windows/hardware/ff559020) 、バッファー内に含まれている構造体**NdisSapParams**します。

**NdisSapParams**  
1 つまたは複数の NDIS_VAR_DATA_DESC 構造体を含む可変長配列を指定します。 各 NDIS_VAR_DATA_DESC 構造体にはの長さと同様に、オフセットが含まれています、 [CO_SAP](https://msdn.microsoft.com/library/windows/hardware/ff545392)構造体。 各 CO_SAP 構造体には、接続指向のクライアントが着信呼び出しを受信できるサービス アクセス ポイント (SAP) を指定します。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

