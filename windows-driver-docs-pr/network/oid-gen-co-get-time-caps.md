---
title: OID_GEN_CO_GET_TIME_CAPS
description: このトピックでは、OID_GEN_CO_GET_TIME_CAPS オブジェクト識別子 (OID) について説明します。
ms.assetid: 6381cfc4-b070-4bd4-90de-6de8a4656cbb
keywords:
- OID_GEN_CO_GET_TIME_CAPS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 230cad6138b9cc7f29eabac631eb0bcc4299f288
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916617"
---
# <a name="oid_gen_co_get_time_caps"></a>OID_GEN_CO_GET_TIME_CAPS

> [!NOTE]
> OID_GEN_CO_GET_TIME_CAPS は OID_GEN_GET_TIME_CAPS と同じです。

OID_GEN_CO_GET_TIME_CAPS OID は、次のように定義されている GEN_GET_TIME_CAPS 構造としてフォーマットされた NIC のローカル時刻をレポートするための機能を返すようにミニポートドライバーに要求します。

```c++
typedef struct _GEN_GET_TIME_CAPS{
    ULONG   Flags;
    ULONG   ClockPrecision;
} GEN_GET_TIME_CAPS, *PGEN_GET_TIME_CAPS;
```

この構造体のメンバーには、次の情報が含まれています。

**フラグ**  
次のフラグは、組み合わせて使用できます。 指定されていないフラグはすべて0に設定する必要があります。 

READABLE_LOCAL_CLOCK  
設定すると、NIC に読み取り可能なクロックが存在することを示します。 このようなハードウェアクロックがなくても、NdisGetCurrentSystemTime を呼び出すことでミニポートドライバーはシステムクロックを使用できます。これは、ClockPrecision メンバーの正しい有効桁数を報告する場合に限ります。

CLOCK_NETWORK_DERIVED  
設定すると、NIC のローカル時刻がネットワーク接続から取得されることを示します。これは、無料で実行できるオンボードクロックとは対照的です。

CLOCK_PRECISION  
設定すると、ClockPrecision メンバーに有効な情報が含まれていることを示します。

RECEIVE_TIME_INDICATION_CAPABLE  
設定されている場合、NIC ハードウェアは、受信した PDU の最初のセルを受信するローカル時刻を記録できます。また、プロトコルにパケットを示すときに、ミニポートドライバーが各 PDU に対してこの受信時間を反映することを示します。

TIMED_SEND_CAPABLE  
設定すると、NIC がローカル時刻に従ってパケットを送信するようにスケジュールできることを示します。 プロトコルでは NDIS_SET_PACKET_TIME_TO_SEND を使用して、パケット記述子の帯域外データブロックに TimeToSend タイムスタンプを設定できます。 タイムスタンプを設定しても、パケットが実際に送信されるときには影響を与えません。代わりに、タイムスタンプが記録の記録に使用されます。 プロトコルドライバーは、タイムスタンプを使用して、パケットの送信を完了するためにかかる時間を判断できます。

TIME_STAMP_CAPABLE  
設定されている場合、NIC が (送信パケットの適切なフィールドに) パケットの最初のバイトが送信される時刻をスタンプでき、NIC が受信パケットの同じフィールドからこの時間を取得できることを示します。

**ClockPrecision**  
1億あたりの部分のクロック精度を指定します。 この情報が有効と見なされるようにするには、CLOCK_PRECISION フラグを設定する必要があります。

## <a name="remarks"></a>注釈

ミニポートドライバーでは、ローカルまたはネットワーククロックがない場合でも、特定のタイミングパラメーターがサポートされます。 特に、ミニポートドライバーでは、受信時間の表示、時間指定の送信、さらにはタイムスタンプにシステムクロックを使用できます。 NIC ベースのクロックは、有効桁数が高く、システムクロックより短い待機時間でアクセスできる可能性が高いため、より優れています。 どのような場合でも、ミニポートドライバーは、使用するクロックの有効桁数を指定する必要があります。 これにより、プロトコルは、ミニポートドライバーのタイミングサポートを最適に使用する方法を決定できます。

ミニポートドライバーが読み取り可能なクロックの存在を報告する場合は、OID_GEN_GET_NETCARD_TIME クエリにすぐに応答できるように準備する必要があります。 この呼び出しに対するミニポートドライバーの応答は時間が重要であるため、同期する必要があります。


## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

