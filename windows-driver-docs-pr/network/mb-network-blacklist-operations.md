---
title: MB ネットワーク ブラックリスト操作
description: MB ネットワーク ブラックリスト操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8b839edae59e50126b399cb0018573180281ba5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343294"
---
# <a name="mb-network-blacklist-operations"></a>MB ネットワーク ブラックリスト操作

デバイスは、特定の SIM カードが挿入されると、特定のネットワークに登録するデバイスがしないかどうかなど、さまざまなシナリオでのネットワークに登録する必要があります。 これらの状況では、Windows 10、バージョンを処理するには、1703 は SIM カードやネットワーク プロバイダーにブラック リストを構成する OS を有効にするモデム インターフェイスを追加します。

いつでもでも、OS は、SIM またはネットワークをデバイスは登録が許可されなかったを指定するモデムで MCC/mnc もペアを構成できます。  インターフェイスは、ネットワーク プロバイダーの 2 つの異なるリスト、別および SIM プロバイダーは、1 つを許可するのに十分な柔軟性があります。  SIM またはネットワークの特定のプロバイダーがブラック リストに掲載されているために、デバイスは登録を試行しなかった、拒否された、モデムは登録状態を報告する必要があります。

## <a name="mb-interface-update-for-network-blacklist-operations"></a>ブラック リストのネットワーク操作の MB インターフェイスの更新プログラム

OS を照会して使用するモデムでは、一致する SIM カードのときに登録することはできませんまたはネットワーク プロバイダーは、デバイス上に存在する MCC と mnc もペアの設定を有効にするのには、新しい MBIM コマンドが用意されています。 このコマンドでは、MBIM_CID_MS_NETWORK_BLACKLIST として新しい MSFT 独自 CID が定義されています。

サービス名 = **Basic 拡張機能の接続**

UUID = **UUID_BASIC_CONNECT_EXTENSIONS**

UUID 値 = **3d01dcc5 fef5-4 d 05-0d3abef7058e9aaf**

| CID | コマンド コード | 最小 OS バージョン |
| --- | --- | --- |
| MBIM_CID_MS_NETWORK_BLACKLIST | 2 | Windows 10 Version 1703 |

## <a name="mbimcidmsnetworkblacklist"></a>MBIM_CID_MS_NETWORK_BLACKLIST

### <a name="description"></a>説明

SIM カードとネットワークを登録するモデムは望まれていませんが、企業、ユーザーまたはモバイルの演算子を指定できます。 このコマンドを照会して、モデム、ブラック リストを設定できるように、OS に使用されます。 ブラック リストの 2 つあります。

1.  SIM カードのブラック リスト – SIM カードのプロバイダーのブラック リストのメンバーであるを任意のネットワーク上のレジスタを許可しない必要があります。
2.  ネットワーク プロバイダーのブラック リスト – どの SIM カードがデバイス上に存在に関係なく登録する、ブラック リスト上のネットワークを許可しない必要があります。

モデムは、SIM スワップの間で保持およびサイクルの電源をモデムごとの両方のブラック リストを維持する必要があります。 両方のブラック リストにアクセスするクエリまたはセットに SIM 状態に関係なく、すべての時間します。

セットのコマンドは、既存の上書きと予想されてブラック リスト Set コマンドのペイロードでモデムにします。

#### <a name="query"></a>クエリ

MBIM_MS_NETWORK_BLACKLIST_INFO、InformationBuffer で完了したクエリと一連のメッセージが返されます。 クエリの場合は、InformationBuffer は NULL です。

#### <a name="set"></a>Set

セットに対して、InformationBuffer には、MBIM_MS_NETWORK_BLACKLIST_INFO が含まれています。 設定操作でモデムに mnc も/MCC 組み合わせの一覧を指定する必要があります。 SIM カードの IMSI には、指定された mnc もと MCC の値が一致すると、モデムは、ネットワークからの登録を解除する必要があります、mnc も/MCC に一致しない新しい SIM カードが挿入されるまでに再登録しないでください。

#### <a name="unsolicited-event"></a>要請されていないイベント

ブラック リストの状態のいずれかから変更されていない作動に作動要請されていないイベントが発生またはその逆の場合たとえば、次のように、SIM には、プロバイダーのプロバイダーの SIM ブラック リストに一致が挿入される場合です。

### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_MS_NETWORK_BLACKLIST_INFO | 該当なし | 該当なし |
| 応答 | MBIM_MS_NETWORK_BLACKLIST_INFO | MBIM_MS_NETWORK_BLACKLIST_INFO | MBIM_MS_NETWORK_BLACKLIST_INFO |

### <a name="data-structures"></a>データ構造体

#### <a name="query"></a>クエリ

InformationBuffer は NULL にするものとし、InformationBufferLength を 0 にする必要があります。

#### <a name="set"></a>Set

次の MBIM_MS_NETWORK_BLACKLIST_INFO 構造、InformationBuffer で使用されます。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | BlacklistState | MBIM_MS_NETWORK_BLACKLIST_STATE | その結果、ネットワークに登録しないモデムで満たされる条件がブラック リストのいずれかどうかを示します。 詳細については、MBIM_MS_NETWORK_BLACKLIST_STATE テーブルを参照してください。 |
| 4 | 4 | ElementCount (EC) | UINT32 | 後に、DataBuffer にカウントの MBIM_MS_NETWORK_BLACKLIST_PROVIDER 構造体。 |
| 8 | 8 * EC | BlacklistProviderRefList | OL_PAIR_LIST | ペアの最初の要素は 4 バイトのオフセット、MBIM_MS_NETWORK_BLACKLIST_PROVIDER 構造体をこの MBIM_MS_NETWORK_BLACKLIST_INFO 構造体の先頭 (オフセット 0) から計算されます。 詳細については、MBIM_MS_NETWORK_BLACKLIST_PROVIDER テーブルを参照してください。  ペアの 2 番目の要素は、対応する MBIM_MS_NETWORK_BLACKLIST_PROVIDER 構造へのポインターのサイズが 4 バイトです。 |
| 8 + (8 * EC) |  | DataBuffer | DATABUFFER | MBIM_MS_NETWORK_BLACKLIST_PROVIDER 構造体の配列。 |

上記の表に、次のデータ構造が使用されます。

MBIM_MS_NETWORK_BLACKLIST_STATE では、2 つの異なるブラック リストの考えられる状態について説明します。

| 種類 | ［マスク］ | 説明 |
| --- | --- | --- |
| MbimMsNetworkBlacklistStateNotActuated | 0 h | ブラック リストの両方の条件が満たされていません。 |
| MbimMsNetworkBlacklistSIMProviderActuated | 1 時間 | プロバイダー ID には、SIM プロバイダー ID のブラック リストが一致するように挿入された SIM がブラックします。 |
| MbimMsNetworkBlacklistNetworkProviderActuated | 2 時間 | 使用可能なネットワークがブラック リストに掲載のプロバイダー Id はすべてプロバイダーの id。 ネットワークのブラック リストにあるので |

MBIM_MS_NETWORK_BLACKLIST_PROVIDER では、ブラック リストのプロバイダーを指定します。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | MCC | UINT32 | 3 gpp により指定に従って、MCC は IMSI の一部であるし、プロバイダーの国を指定します。 |
| 4 | 4 | MNC | UINT32 | 3 gpp により指定に従って、mnc もは IMSI の一部であるし、プロバイダーのネットワークを指定します。 |
| 8 | 4 | NetworkBlacklistType | MBIM_MS_NETWORK_BLACKLIST_TYPE | MCC/mnc もペアをブラック リストの種類が使用されているを指定します。 詳細については、MBIM_MS_NETWORK_BLACKLIST_TYPE テーブルを参照してください。 |

MBIM_MS_NETWORK_BLACKLIST_TYPE は、前のデータ構造で使用されます。 これは、2 つのブラック リストのどちらを使用するを指定します。

| 種類 | Value | 説明 |
| --- | --- | ---- |
| MbimMsNetworkBlacklistTypeSIM | 0 | MCC/mnc もペアは、SIM プロバイダーのブラック リストに使用されます。 |
| MbimMsNetworkBlacklistTypeNetwork | 1 | MCC/mnc もペアは、ネットワーク プロバイダーのブラック リストに使用されます。 |

#### <a name="response"></a>応答

詳細については、MBIM_MS_NETWORK_BLACKLIST_INFO テーブルを参照してください。

### <a name="status-codes"></a>状態コード

クエリおよびセットの操作。

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_READ_FAILURE | デバイスがプロビジョニングされているコンテキストを取得できなかったため、操作が失敗しました。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | デバイスは、操作をサポートしていないため、操作が失敗しました。 |

セット操作の場合のみ。

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_INVALID_PARAMETERS | 無効なパラメーターのため、操作が失敗しました。 |
| MBIM_STATUS_WRITE_FAILURE | 更新の要求が成功した操作が失敗しました。 |
