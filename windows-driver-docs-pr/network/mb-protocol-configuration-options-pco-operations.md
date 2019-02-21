---
title: MB プロトコルの構成オプション (PCO) 操作
description: MB プロトコルの構成オプション (PCO) 操作
ms.assetid: 682C507C-5B2C-45E3-99D2-EEC68F8FC715
keywords:
- MB PCO オプション、モバイル ブロード バンド PCO オプションは、プロトコルの構成オプションの MB、モバイル ブロード バンドのプロトコルの構成オプション、WDK ネットワーク ドライバー、MBB ミニポート ドライバー
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: f149f51566190780a910ce6e876cf7ee420b8b66
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551871"
---
# <a name="mb-protocol-configuration-options-pco-operations"></a>MB プロトコルの構成オプション (PCO) 操作

## <a name="overview"></a>概要

これまでは、プロトコルの構成オプション (PCO) の値について Windows NDIS 定義は、モデムとネットワークから完全 PCO 値を今後可能性のある受信するための汎用されています。 時点で、Windows 10 バージョン 1709 では、ただし、いくつかモデムはのみ、OS に特定 PCO 要素の演算子を渡すことができます。 このトピックでは、現在演算子の特定の専用 PCO 実装の動作を定義します。

ホストに PCO 値を渡すは 3 つのシナリオがあります。
1.  アクティブな接続を新しい PCO 値が到着する場合
2.  アプリやサービスがモデムから最新の PCO 値をクエリした場合
3.  接続のブリッジまたは既に最初の時間と PCO 値に対してアクティブ化の場合は、モデムに存在します。

最初のシナリオでは、モデムに送信する必要があります、 [NDIS_STATUS_WWAN_PCO_STATUS](ndis-status-wwan-pco-status.md)新しい PCO 値が適切な NDIS ポート番号を持つ、ネットワークから受信されたときに、新しい PCO 値の変更を示す OS への通知対応する PDN を表します。 バッテリを不必要にドレインを避けるためには、モデム避ける必要があります、ノイズの多い通知」の説明に従って[モデムの動作をセレクティブ サスペンドとコネクト スタンバイ](#modem-behavior-with-selective-suspend-and-connected-standby)します。

2 番目のシナリオでは、PDN のアクティブな接続、モデムから PCO 値に、アプリまたはサービスが照会するとき、ホストは送信、モデム、 [OID_WWAN_PCO](oid-wwan-pco.md)を最新のクエリ要求キャッシュ、モデムで PCO 値。

3 番目のシナリオでは、接続がアクティブ化またはホストで、ブリッジとモデムの送信先、 **NDIS_STATUS_WWAN_PCO_STATUS**ブリッジまたはアクティブ接続のモデムで PCO 値が既に存在する場合に通知します要求ホスト。 通知は、対応する PDN の NDIS ポート番号渡す必要があります。

次の図は、シナリオの流れを示しています。

![MB PCO 操作フロー](images/mb_PCO_operations_flow.png "MB PCO 操作フロー")

## <a name="modem-behavior-with-selective-suspend-and-connected-standby"></a>セレクティブ サスペンド、コネクト スタンバイとモデムの動作

セレクティブ サスペンドを有効にすると、モデムは、ネットワークから PCO データ構造体を受信するたびに、OS を通知できます。 ただし、モデムは、不要なデバイスのウェイク アップを避ける必要があります。 それ以外の場合、ネットワークからのノイズの多い PCO 通知は、デバイスを頻繁にウェイク アップされ、バッテリが不必要に消費されます。

コネクト スタンバイを有効にすると、モデムはしないでくださいがウェイク アップのデバイスだけでなく、ウェイク アップは必要はありません、OS もあるため、ネットワークから PCO データ構造体を受け取ると、OS を通知します。 代わりに、モデムをデータ構造体からのすべての最新 PCO 要素をキャッシュして、OS は、コネクト スタンバイを終了すると、OS に通知します。 MBIM モデムの場合は、PCO データ構造のすべてをキャッシュする必要があり、のみ、ホストがサブスクライブした後、OS に PCO 通知を送信します。 これは、実行するシステムの電源がコネクト スタンバイの後に電源を完全に返されるときに、MBIM_CID_DEVICE_SERVICE_SUBSCRIBE_LIST CID を使用します。

## <a name="resetting-the-modem-based-on-pco-values"></a>PCO 値に基づいて、モデムをリセットします。

ネットワークから受信した PCO 値に基づいて、次のシナリオでモデムがリセットされます。

1.  PCO の受信後に完了したユーザーのセルフ ライセンス認証、ネットワークから 5 を = です。 新しい PCO 値が送信されます (3、0、または何もモバイル事業者アプリを認識できます) は、OS に、OS に渡すモバイル事業者アプリ。
2.  ユーザーが多いクレジットを追加 PCO を受信した後、自分のアカウントに 3 を = です。 新しい PCO 値が送信されますが (0、または何もモバイル事業者アプリを認識できます)、OS に、OS に渡すモバイル事業者アプリ。

ホストでは、ホストからのアクティブ化された接続を無効化しないと、モデムにリセットした後、PDN との接続を再確立する必要がありますに自動的にリセットされるモデムの認識しません。 接続を確立すると、新しい受信 PCO 値をネットワークから受信、モデムは、要請していない、 [NDIS_STATUS_WWAN_PCO_STATUS](ndis-status-wwan-pco-status.md)ホストに通知します。

次の図は、これらのシナリオのいずれかが発生した場合、月の例と Verizon のワイヤレスとモデムのリセット フローを示しています。

![MB モデム PCO 値に基づいてリセット](images/mb_PCO_modem_reset.png "MB モデム PCO 値に基づいてリセット")

## <a name="ndis-interface-to-the-modem"></a>モデムの NDIS インターフェイス

状態と PCO 値演算子のネットワークから受信したモデムのペイロードのクエリを実行するには、次を参照してください。 [OID_WWAN_PCO](oid-wwan-pco.md)します。 **OID_WWAN_PCO**を使用して、 [ **NDIS_WWAN_PCO_STATUS** ](https://msdn.microsoft.com/library/windows/hardware/C71187C5-74B6-450A-8461-BB9FDF60DB8D)を格納する構造体、 [ **WWAN_PCO_VALUE** ](https://msdn.microsoft.com/library/windows/hardware/45A499CE-2C9A-4070-BEF8-880E7673FA8E) ネットワークから PCO 情報のペイロードを表す構造体。

モデムの現在の PCO 状態の OS を通知するために、モデムのミニポート ドライバーによって送信された状態の通知を参照してください。 [NDIS_STATUS_WWAN_PCO_STATUS](ndis-status-wwan-pco-status.md)します。

## <a name="mb-cid-to-the-modem"></a>モデムに CID を MB

サービス = **MBB_UUID_BASIC_CONNECT_EXT_CONSTANT**

サービスの UUID = **3d01dcc5-fef5-4d05-0d3a-bef7058e9aaf**

PCO は、次の Cid が定義されています。

| CID | コマンド コード | 最小 OS バージョン |
| --- | --- | --- |
| MBIM_CID_PCO | 9 | Windows 10 バージョン 1709 |

### <a name="mbimcidpco"></a>MBIM_CID_PCO

このコマンドは、通信事業者ネットワークからモデムにキャッシュされている PCO データの照会に使用されます。

#### <a name="query"></a>クエリ

含まれています、InformationBuffer、 **MBIM_PCO_VALUE**のみに関連するフィールドが*SessionId*します。 *SessionId*は将来使用するために予約されていると、常に Windows 10 バージョン 1709 では 0 になります。 *SessionId*クエリで示す IP PCO 値のデータ ストリームが、関数によって返されます。 

#### <a name="set"></a>設定

適用できません。

#### <a name="unsolicited-event"></a>要請されていないイベント

要請されていないイベントは、MBIM_PCO_VALUE を含み、新しい PCO 値が、アクティブな接続で到着したときに送信されます。

#### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 該当なし | MBIM_PCO_VALUE | 該当なし |
| 応答 | 該当なし | MBIM_PCO_VALUE | MBIM_PCO_VALUE |

#### <a name="data-structures"></a>データ構造体

##### <a name="mbimpcotype"></a>MBIM_PCO_TYPE

| 種類 | Value | 説明 |
| --- | --- | --- |
| MBIMPcoTypeComplete | 0 | ネットワークから受信した渡される完全な PCO 構造ヘッダーが現実的 PCO 構造体の 8 ビット 3 に、3 gpp TS24.008 仕様で定義されているプロトコルを反映するよう指定します。 |
| MBIMPcoTypePartial | 1 | モデムがネットワークから受信した PCO 構造のサブセットを渡すことだけを指定します。 ヘッダーには、3 gpp TS24.008 仕様で定義されている PCO 構造が一致するが、3 のオクテットの"Configuration protocol"は有効なできない可能性があります。 |

##### <a name="mbimpcovalue"></a>MBIM_PCO_VALUE

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | セッション Id | UINT32 | クエリで SessionId 示します IP PCO 値のデータ ストリームが、関数によって返されます。 |
| 4 | 4 | PcoDataSize | UINT32 | 0 ~ 256 PcoData の長さ。 この値は、クエリで 0 になります。 |
| 8 | 4 | PcoDataType | UINT32 | PCO データ型。 詳細については、次を参照してください。 [MBIM_PCO_TYPE](#mbimpcotype)します。 |
| 12 | | PcoDataBuffer | DATABUFFER | 3 gpp TS24.008 仕様から PCO 構造体。 |

#### <a name="status-codes"></a>状態コード

この CID は、汎用的な状態コードのみを使用します。
