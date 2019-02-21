---
title: OID_GEN_CO_GET_TIME_CAPS
description: このトピックでは、OID_GEN_CO_GET_TIME_CAPS オブジェクト識別子 (OID) について説明します。
ms.assetid: 6381cfc4-b070-4bd4-90de-6de8a4656cbb
keywords:
- OID_GEN_CO_GET_TIME_CAPS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 574b33cce46ddbd0f1b745cc154c6901f9e819d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538219"
---
# <a name="oidgencogettimecaps"></a>OID_GEN_CO_GET_TIME_CAPS

> [!NOTE]
> OID_GEN_CO_GET_TIME_CAPS では、OID_GEN_GET_TIME_CAPS と同じです。

OID_GEN_CO_GET_TIME_CAPS OID は、その機能が次のように定義されている GEN_GET_TIME_CAPS 構造体として書式設定された NIC のローカル時刻をレポートを返すミニポート ドライバーを要求します。

```c++
typedef struct _GEN_GET_TIME_CAPS{
    ULONG   Flags;
    ULONG   ClockPrecision;
} GEN_GET_TIME_CAPS, *PGEN_GET_TIME_CAPS;
```

この構造体のメンバーには、次の情報が含まれます。

**フラグ**  
次のフラグは、論理和を共存することができます。 指定されていないすべてのフラグは、0 に設定する必要があります。 

READABLE_LOCAL_CLOCK  
設定すると、NIC で読み取り可能なクロックのプレゼンスを示す このようなハードウェア クロックでは、しなくてもミニポート ドライバーは ClockPrecision メンバーの適切な有効桁数を報告する限り、NdisGetCurrentSystemTime を呼び出すことによって、システム クロックを使用できます。

CLOCK_NETWORK_DERIVED  
設定すると、NIC の現地時刻がネットワーク接続、無料の実行ではなくオンボード クロックから派生したことを示します。

CLOCK_PRECISION  
設定すると、ClockPrecision メンバーに有効な情報が含まれていることを示します。

RECEIVE_TIME_INDICATION_CAPABLE  
設定すると、NIC ハードウェアで受信された PDU の最初のセルを受け取るし、ミニポート ドライバーにはこれが反映されますを受信時間ごとの PDU のパケットのプロトコルを指定する際にローカル時刻に注意してくださいできることを示します。

TIMED_SEND_CAPABLE  
設定すると、NIC がパケットをローカル時刻に従って転送をスケジュールできますを示します。 プロトコルは、パケットの記述子の帯域外のデータ ブロックで TimeToSend タイムスタンプを設定するのに NDIS_SET_PACKET_TIME_TO_SEND を使用できます。 タイムスタンプを設定する場合は影響しませんパケットは実際に送信されます。代わりに、タイムスタンプは、記録に使用されます。 プロトコル ドライバーは、パケットの送信を完了にかかる時間を決定するのにタイムスタンプを使用できます。

TIME_STAMP_CAPABLE  
設定すると、いる NIC できますスタンプ (発信パケットの適切なフィールド) で時刻を示します、パケットの最初のバイトが転送され、NIC が着信パケットの同じフィールドからこの時間を取得できます。

**ClockPrecision**  
ごとの部分でクロックの有効桁数を指定, 000, 000 です。 この情報が有効と見なされるには、CLOCK_PRECISION フラグを設定する必要があります。

## <a name="remarks"></a>注釈

ミニポート ドライバーでは、特定のパラメーターがない場合、ローカルまたはネットワーク クロックであってもタイムアウトにサポートを提供できます。 ミニポート ドライバーが、システム クロックを使用して具体的には、時間がない、時間の送信およびもタイムスタンプが表示されます。 高い精度を提供し、待ち時間が短く、システム クロックよりも使用アクセスできる可能性があるために、NIC に基づくクロックの使用をお勧めします。 場合は、ミニポート ドライバーが使用するクロックの有効桁数を指定する必要があります。 これにより、ミニポート ドライバーのタイミングのサポートを活用する方法を決定するプロトコルです。

ミニポート ドライバーでは、読み取り可能なクロックのプレゼンスを報告する場合は、すぐに OID_GEN_GET_NETCARD_TIME のクエリに応答する準備する必要があります。 この呼び出しに、ミニポート ドライバーの応答は、タイム クリティカル同期したがってする必要があります。


## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

