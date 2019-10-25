---
title: OID_CO_TAPI_TRANSLATE_TAPI_SAP
description: このトピックでは、OID_CO_TAPI_TRANSLATE_TAPI_SAP オブジェクト識別子 (OID) について説明します。
ms.assetid: 701a1d02-8528-4b61-adbb-97c817194ac7
keywords:
- OID_CO_TAPI_TRANSLATE_TAPI_SAP
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: c257d84f9ff3b34a23b0685d4a170f3cd4145a29
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844947"
---
# <a name="oid_co_tapi_translate_tapi_sap"></a>OID_CO_TAPI_TRANSLATE_TAPI_SAP

OID_CO_TAPI_TRANSLATE_TAPI_SAP OID は、TAPI 呼び出しパラメーターから1つ以上の Sap を準備するために、呼び出しマネージャーまたは統合された MCM ドライバーを要求します。 この OID に対してクエリを行うクライアントは、呼び出しマネージャーまたは MCM ドライバーによって返される NDIS SAP を[NdisClRegisterSap](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclregistersap)に入力 ( [CO_SAP](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545392(v=vs.85))構造として書式設定されたもの) として使用します。これにより、クライアントはを呼び出して、着信呼び出しを受信する SAP を登録します。

この要求では、次のように定義されている CO_TAPI_TRANSLATE_SAP 構造体を使用します。

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

この構造体のメンバーには、次の情報が含まれています。

**ulLineID**  
0から始まる行識別子を指定します。

**ulAddressID**  
**UlLineID**によって指定された行の0から始まるアドレス識別子を指定します。

**ulMediaModes**  
次の1つまたは複数の LINEMEDIAMODE_constants として、クライアントが関心のある呼び出しの情報ストリームのメディアモードを指定します。 

- **LINEMEDIAMODE_UNKNOWN**  
メディアストリームは存在しますが、そのモードは現在不明であり、後で認識される可能性があります。 これは、メディアの種類が未分類の呼び出しに対応します。 一般的なアナログテレフォニー環境では、着信呼び出しのメディアモードは、呼び出しに応答し、メディアストリームがフィルター処理されて確認されるまで不明な場合があります。 

    **LINEMEDIAMODE_UNKNOWN**フラグが設定されている場合は、他のメディアフラグも設定できます。 これは、メディアが不明であることを示していますが、他のメディアモードのいずれかになっている可能性があります。

- **LINEMEDIAMODE_INTERACTIVEVOICE**  
通話に音声エネルギーが存在し、通話が両方のエンドで人間との対話型呼び出しとして扱われます。

- **LINEMEDIAMODE_AUTOMATEDVOICE**  
通話に音声エネルギーが存在し、音声は自動アプリケーションによってローカルで処理されます。

- **LINEMEDIAMODE_DATAMODEM**  
呼び出しのデータモデムセッション。

- **LINEMEDIAMODE_G3FAX**  
グループ3の fax が通話で送受信されています。

- **LINEMEDIAMODE_G4FAX**  
グループ4の fax が、通話で送信または受信されています。

- **LINEMEDIAMODE_TDD**  
呼び出しの TDD (聴覚の電気通信デバイス)。

- **LINEMEDIAMODE_DIGITALDATA**  
デジタルデータは、通話で送信または受信されています。

- **LINEMEDIAMODE_TELETEX**  
呼び出しの teletex セッション。 (Teletex はテレマティクスサービスの1つです)。

- **LINEMEDIAMODE_VIDEOTEX**  
呼び出しの videotex セッション。 (Videotex はテレマティクスサービスの1つです)。

- **LINEMEDIAMODE_TELEX**  
呼び出しのテレックスセッション。 (テレックスはテレマティクスサービスの1つです)。

- **LINEMEDIAMODE_MIXED**  
呼び出しのセッションが混在しています。 (Mixed は ISDN テレマティクスサービスの1つです)。

- **LINEMEDIAMODE_ADSI**  
呼び出しの ADSI (アナログディスプレイサービスインターフェイス) セッション。

- **LINEMEDIAMODE_VOICEVIEW**  
通話のメディアモードは VoiceView です。

**確保**  
これは予約されています。 クライアントは、このフィールドを0に設定する必要があります。

**NumberOfSaps**  
**NdisSapParams**のバッファーに格納されている[NDIS_VAR_DATA_DESC](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559020(v=vs.85))構造体の数を指定します。

**NdisSapParams**  
1つ以上の NDIS_VAR_DATA_DESC 構造体を含む可変長配列を指定します。 各 NDIS_VAR_DATA_DESC 構造体には、 [CO_SAP](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545392(v=vs.85))構造体の長さに加えて、へのオフセットが含まれています。 各 CO_SAP 構造体は、接続指向クライアントが着信呼び出しを受信できるサービスアクセスポイント (SAP) を指定します。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis (Ndis .h を含む) |

