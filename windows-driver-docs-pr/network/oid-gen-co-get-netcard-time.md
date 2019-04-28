---
title: OID_GEN_CO_GET_NETCARD_TIME
description: このトピックでは、OID_GEN_CO_GET_NETCARD_TIME オブジェクト識別子 (OID) について説明します。
ms.assetid: 4dfa0f02-2b37-4b9f-95fe-dd33774dedbc
keywords:
- OID_GEN_CO_GET_NETCARD_TIME
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd55b2703f6b691084f8928de0dcd8ec6e564f6f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379250"
---
# <a name="oidgencogetnetcardtime"></a>OID_GEN_CO_GET_NETCARD_TIME

> [!NOTE]
> OID_GEN_CO_GET_NETCARD_TIME では、OID_GEN_GET_NETCARD_TIME と同じです。

OID_GEN_CO_GET_NETCARD_TIME OID は、NIC でのクロックからまたはネットワークからの派生として、NIC の現地時刻を返すミニポート ドライバーを要求します。 時刻形式は次のように定義されている GEN_GET_NETCARD_TIME 構造体としてです。

```c++
typedef struct _GEN_GET_NETCARD_TIME{
    ULONGLONG   ReadTime;
} GEN_GET_NETCARD_TIME, *PGEN_GET_NETCARD_TIME;
```

この構造体のメンバーには、次の情報が含まれています。

**ReadTime**  
    NIC の現地時刻。

## <a name="remarks"></a>注釈

ミニポート ドライバーでは、そのローカル時刻の単位を指定する、 **ClockPrecision**ミニポート ドライバーが前の OID_GEN_CO_GET_TIME_CAPS クエリ応答で返される GEN_GET_TIME_CAPS 構造体の要素。

ミニポート ドライバーでは、READABLE_LOCAL_CLOCK フラグを設定、OID_GEN_CO_GET_TIME_CAPS クエリへの応答、NIC はオンボードのクロックからのローカル時刻を派生します。 ミニポート ドライバーでは、CLOCK_NETWORK_DERIVED フラグを設定、OID_GEN_CO_GET_TIME_CAPS クエリへの応答、NIC は、ネットワークからのローカル時刻を派生します。

ミニポート ドライバーがごとの部分でクロックの精度を報告できるローカル時刻がオンボードのクロックから派生の場合, 000, 000 です。 一般より正確なする可能性があり、同じネットワーク スイッチに接続されている多くのマシンの同期に使用できるためは、ネットワークから派生したクロックは、ことをお勧めします。

ミニポート ドライバー返す必要があります、現地時刻に同期的に OID_GEN_CO_GET_NETCARD_TIME クエリへの応答ため、このクエリは、NIC の現地時刻とプロトコル ドライバーを同期します。 プロトコル ドライバーは、応答時間の待機時間を除外する連続 OID_GEN_CO_GET_NETCARD_TIME クエリ数回を送信する必要があります。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

