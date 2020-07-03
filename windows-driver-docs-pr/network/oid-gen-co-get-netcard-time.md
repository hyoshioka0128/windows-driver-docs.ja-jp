---
title: OID_GEN_CO_GET_NETCARD_TIME
description: このトピックでは、OID_GEN_CO_GET_NETCARD_TIME オブジェクト識別子 (OID) について説明します。
ms.assetid: 4dfa0f02-2b37-4b9f-95fe-dd33774dedbc
keywords:
- OID_GEN_CO_GET_NETCARD_TIME
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 944ba507a1b12bdad15c5d55676d9f8fbdead1ab
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916620"
---
# <a name="oid_gen_co_get_netcard_time"></a>OID_GEN_CO_GET_NETCARD_TIME

> [!NOTE]
> OID_GEN_CO_GET_NETCARD_TIME は OID_GEN_GET_NETCARD_TIME と同じです。

OID_GEN_CO_GET_NETCARD_TIME OID は、NIC またはネットワークからのクロックからの派生として、NIC のローカル時刻を返すようにミニポートドライバーに要求します。 時刻は、次のように定義された GEN_GET_NETCARD_TIME 構造体として書式設定されます。

```c++
typedef struct _GEN_GET_NETCARD_TIME{
    ULONGLONG   ReadTime;
} GEN_GET_NETCARD_TIME, *PGEN_GET_NETCARD_TIME;
```

この構造体のメンバーには、次の情報が含まれています。

**Readtime だけ**  
    NIC のローカル時刻。

## <a name="remarks"></a>注釈

ミニポートドライバーは、前の OID_GEN_CO_GET_TIME_CAPS クエリに応答して、ミニポートドライバーが返す GEN_GET_TIME_CAPS 構造体の**Clockprecision**要素のローカル時刻の単位を指定しました。

ミニポートドライバーによって、OID_GEN_CO_GET_TIME_CAPS クエリへの応答に READABLE_LOCAL_CLOCK フラグが設定されている場合、NIC はオンボードクロックからローカル時刻を取得します。 ミニポートドライバーによって、OID_GEN_CO_GET_TIME_CAPS クエリへの応答で CLOCK_NETWORK_DERIVED フラグが設定されている場合、NIC はネットワークからローカル時刻を取得します。

現地時刻がオンボードクロックから派生している場合、ミニポートドライバーは、100万単位でクロック精度を報告できる必要があります。 一般に、ネットワークから派生した時計はより正確であり、同じネットワークまたはスイッチに接続されている多数のコンピューターを同期するために使用できるため、より適しています。

ミニポートドライバーは、OID_GEN_CO_GET_NETCARD_TIME クエリに応答してローカル時刻を同期的に返す必要があります。このクエリでは、プロトコルドライバーが NIC のローカル時刻と同期されるためです。 プロトコルドライバーは、OID_GEN_CO_GET_NETCARD_TIME クエリを連続して複数回送信して、応答時間の待ち時間をフィルターで除外する必要があります。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

