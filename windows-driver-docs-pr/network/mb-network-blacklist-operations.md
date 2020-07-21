---
title: MB ネットワーク ブラックリスト操作
description: MB ネットワーク ブラックリスト操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba4fe888402bc5e5ec3fd22439f14dd66cb16065
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557721"
---
# <a name="mb-network-blacklist-operations"></a>MB ネットワーク ブラックリスト操作

特定の SIM カードが挿入された場合や、デバイスが特定のネットワークに登録されたくない場合など、さまざまなシナリオで、デバイスがネットワークに登録されていないことが必要になることがあります。 このような状況に対処するために、Windows 10 バージョン1703はモデムインターフェイスを追加して、OS が SIM カードおよびネットワークプロバイダー用にブラックリストを構成できるようにします。

いつでも、OS は、デバイスの登録を許可されていない SIM またはネットワークを指定するために、モデムの MCC/MNC ペアを構成できます。  インターフェイスは、2つの異なるリストを許可するのに十分な柔軟性を備えています。1つは SIM プロバイダー用で、もう1つはネットワークプロバイダー用です。  特定の SIM またはネットワークプロバイダーがブラックリストされているためにデバイスが登録を試行しなかった場合、モデムは登録ステータスを [拒否] として報告する必要があります。

## <a name="mb-interface-update-for-network-blacklist-operations"></a>ネットワークブラックリスト操作のための MB インターフェイスの更新

新しい MBIM コマンドが作成されました。これにより、OS は、一致する SIM カードまたはネットワークプロバイダーがデバイス上に存在する場合に、モデムが登録を試行しないように、MCC と MBIM のペアを設定できます。 このコマンドでは、新しい MSFT 専有 CID が MBIM_CID_MS_NETWORK_BLACKLIST として定義されています。

サービス名 =**基本接続拡張機能**

UUID = **UUID_BASIC_CONNECT_EXTENSIONS**

UUID 値 = **3d01dcc5-fef5-4d05-0d3abef7058e9aaf**

| CID | コマンド コード | 最小 OS バージョン |
| --- | --- | --- |
| MBIM_CID_MS_NETWORK_BLACKLIST | 2 | Windows 10 Version 1703 |

## <a name="mbim_cid_ms_network_blacklist"></a>MBIM_CID_MS_NETWORK_BLACKLIST

### <a name="description"></a>説明

企業、ユーザー、または携帯電話では、モデムを登録したくない SIM カードとネットワークを指定できます。 このコマンドは、OS がモデムのブラックリストを照会して設定できるようにするために使用されます。 次の2つのブラックリストがあります。

1.  SIM カードブラックリスト–プロバイダーがブラックリストのメンバーである SIM カードは、どのネットワークにも登録できないようにする必要があります。
2.  ネットワークプロバイダーのブラックリスト-デバイスにどの SIM カードがあるかに関係なく、ブラックリストのネットワークを登録できないようにする必要があります。

モデムは、モデムごとにブラックリストの両方を維持し、SIM スワップと電源サイクルをまたいで保持する必要があります。 どちらのブラックリストにも、SIM の状態に関係なく、クエリを使用してアクセスしたり、常に設定したりできます。

Set コマンドでは、Set コマンドのペイロードを使用して、モデムの既存のブラックリストを上書きすることが想定されています。

#### <a name="query"></a>クエリ

完了したクエリから MBIM_MS_NETWORK_BLACKLIST_INFO が返され、InformationBuffer にメッセージが設定されます。 クエリの場合、InformationBuffer は NULL になります。

#### <a name="set"></a>オン

Set の場合、InformationBuffer には MBIM_MS_NETWORK_BLACKLIST_INFO が含まれます。 設定操作では、MNC/MCC の組み合わせの一覧をモデムに提供する必要があります。 SIM カードの IMSI が指定された MNC と MCC の値に一致する場合、モデムはネットワークから登録を解除する必要があります。また、MNC/MCC と一致しない新しい SIM カードが挿入されるまで、再登録を試行しないでください。

#### <a name="unsolicited-event"></a>一方的なイベント

ブラックリストの状態のいずれかが、感知から not 感知に変化した場合、またはその逆の場合は、要請されていないイベントが発生します。たとえば、sim が挿入され、プロバイダーが SIM プロバイダーのブラックリストと一致する場合などです。

### <a name="parameters"></a>パラメーター

| 操作 | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_MS_NETWORK_BLACKLIST_INFO | 適用なし | 適用なし |
| 応答 | MBIM_MS_NETWORK_BLACKLIST_INFO | MBIM_MS_NETWORK_BLACKLIST_INFO | MBIM_MS_NETWORK_BLACKLIST_INFO |

### <a name="data-structures"></a>データ構造

#### <a name="query"></a>クエリ

InformationBuffer は NULL にする必要があり、InformationBufferLength は0である必要があります。

#### <a name="set"></a>オン

InformationBuffer では、次の MBIM_MS_NETWORK_BLACKLIST_INFO 構造体を使用する必要があります。

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | BlacklistState | MBIM_MS_NETWORK_BLACKLIST_STATE | ブラックリストの条件のいずれかが満たされ、その結果、モデムがネットワークに登録されていないかどうかを示します。 詳細については、MBIM_MS_NETWORK_BLACKLIST_STATE の表を参照してください。 |
| 4 | 4 | ElementCount (EC) | UINT32 | DataBuffer で後に続く MBIM_MS_NETWORK_BLACKLIST_PROVIDER 構造体の数。 |
| 8 | 8 * EC | BlacklistProviderRefList | OL_PAIR_LIST | ペアの最初の要素は4バイトオフセットで、この MBIM_MS_NETWORK_BLACKLIST_INFO 構造体の先頭 (オフセット 0) から MBIM_MS_NETWORK_BLACKLIST_PROVIDER 構造体に計算されます。 詳細については、MBIM_MS_NETWORK_BLACKLIST_PROVIDER の表を参照してください。  ペアの2番目の要素は、対応する MBIM_MS_NETWORK_BLACKLIST_PROVIDER 構造体へのポインターの4バイトサイズです。 |
| 8 + (8 * EC) |  | DataBuffer | DATABUFFER | MBIM_MS_NETWORK_BLACKLIST_PROVIDER 構造体の配列。 |

前の表では、次のデータ構造が使用されています。

MBIM_MS_NETWORK_BLACKLIST_STATE には、2つの異なるブラックリストの考えられる状態が記述されています。

| 種類 | マスク | 説明 |
| --- | --- | --- |
| MbimMsNetworkBlacklistStateNotActuated | 0h | 両方のブラックリスト条件が満たされていません。 |
| Mbimmsnetworkblacklist、Provider感知 | 1h | プロバイダー ID が SIM プロバイダー ID のブラックリストと一致するため、挿入された SIM はブラックリストです。 |
| MbimMsNetworkBlacklistNetworkProviderActuated | 後半 | 使用可能なネットワークは、プロバイダー Id がすべてブラックリストのネットワークプロバイダー ID であるため、ブラックリストです。 |

MBIM_MS_NETWORK_BLACKLIST_PROVIDER ブラックリストのプロバイダーを指定します。

| Offset | サイズ | フィールド | 型 | [説明] |
| --- | --- | --- | --- | --- |
| 0 | 4 | MCC | UINT32 | 3GPP で指定されているように、MCC は IMSI の一部であり、プロバイダーの国を指定します。 |
| 4 | 4 | MNC | UINT32 | 3GPP で指定されているように、MNC は IMSI の一部であり、プロバイダーのネットワークを指定します。 |
| 8 | 4 | NetworkBlacklistType | MBIM_MS_NETWORK_BLACKLIST_TYPE | MCC/MNC ペアを使用するブラックリストの種類を指定します。 詳細については、MBIM_MS_NETWORK_BLACKLIST_TYPE の表を参照してください。 |

MBIM_MS_NETWORK_BLACKLIST_TYPE は、前のデータ構造体によって使用されます。 2つのブラックリストのどちらを使用するかを指定します。

| 種類 | 値 | 説明 |
| --- | --- | ---- |
| MbimMsNetworkBlacklistTypeSIM | 0 | MCC/MNC ペアは、SIM プロバイダーのブラックリストに使用されます。 |
| MbimMsNetworkBlacklistTypeNetwork | 1 | MCC/MNC ペアは、ネットワークプロバイダーのブラックリストに使用されます。 |

#### <a name="response"></a>応答

詳細については、MBIM_MS_NETWORK_BLACKLIST_INFO の表を参照してください。

### <a name="status-codes"></a>状態コード

クエリおよびセット操作の場合:

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_READ_FAILURE | デバイスがプロビジョニングされたコンテキストを取得できなかったため、操作に失敗しました。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | デバイスで操作がサポートされていないため、操作に失敗しました。 |

Set 操作のみ:

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_INVALID_PARAMETERS | 無効なパラメーターのため、操作に失敗しました。 |
| MBIM_STATUS_WRITE_FAILURE | 更新要求が失敗したため、操作に失敗しました。 |
