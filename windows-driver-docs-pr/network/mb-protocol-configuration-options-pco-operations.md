---
title: MB プロトコル構成オプション (PCO) 操作
description: MB プロトコル構成オプション (PCO) 操作
ms.assetid: 682C507C-5B2C-45E3-99D2-EEC68F8FC715
keywords:
- MB PCO オプション、モバイルブロードバンド PCO オプション、MB プロトコル構成オプション、モバイルブロードバンドプロトコル構成オプション、WDK ネットワークドライバー、MBB ミニポートドライバー
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 943330f5c9db1e0ea7f6261c188364a1077f5029
ms.sourcegitcommit: 2c3b8e0ea0e75b72067d2e22dc530390bc19b11e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2019
ms.locfileid: "67374072"
---
# <a name="mb-protocol-configuration-options-pco-operations"></a>MB プロトコル構成オプション (PCO) 操作

## <a name="overview"></a>概要

従来、プロトコル構成オプション (PCO) の値の Windows NDIS 定義は、将来、モデムとネットワークから完全な PCO 値を受信する可能性があるため、一般的になっていました。 ただし、Windows 10 バージョン1709では、一部のモデムはオペレーター固有の PCO 要素を OS に渡すことしかできません。 このトピックでは、現在のオペレーター固有の PCO 実装の動作を定義します。

PCO 値がホストに渡されるシナリオには、次の3つがあります。
1.  アクティブ化された接続に新しい PCO 値が到着したとき
2.  アプリまたはサービスがモデムからの最新の PCO 値を照会するとき
3.  接続が最初にブリッジまたはアクティブ化され、PCO 値が既にモデムに存在する場合

最初のシナリオでは、新しい pco 値がネットワークから渡されるたびに新しい PCO 値が変更されたことを示す[NDIS_STATUS_WWAN_PCO_STATUS](ndis-status-wwan-pco-status.md)通知を OS に送信し、適切な NDIS ポート番号を指定して、対応する PDN。 不要なバッテリの消耗を避けるために、モデムは、「[セレクティブサスペンドとコネクトスタンバイを使用したモデムの動作](#modem-behavior-with-selective-suspend-and-connected-standby)」で説明されているように、ノイズ通知を回避する必要があります。

2番目のシナリオでは、アプリまたはサービスが、アクティブ化された PDN 接続でモデムから PCO 値に対してクエリを実行すると、ホストはモデムに[OID_WWAN_PCO](oid-wwan-pco.md)クエリ要求を送信し、モデムにキャッシュされた最新の pco 値を読み取ります。

3番目のシナリオでは、ホストで接続がアクティブ化またはブリッジされている場合、ホストから要求されたアクティブな接続またはブリッジ接続の PCO 値が既にモデムに存在するときに、モデムは**NDIS_STATUS_WWAN_PCO_STATUS**通知を送信する必要があります。 通知は、PDN の対応する NDIS ポート番号から渡される必要があります。

次の図は、シナリオフローを示しています。

![MB PCO 操作フロー](images/mb_PCO_operations_flow.png "MB PCO 操作フロー")

## <a name="modem-behavior-with-selective-suspend-and-connected-standby"></a>セレクティブサスペンドとコネクトスタンバイによるモデムの動作

セレクティブサスペンドが有効になっている場合、モデムはネットワークから PCO データ構造を受信するたびに OS に通知できます。 ただし、不要なデバイスウェイクアップを避ける必要があります。 そうしないと、ネットワークからのノイズのある PCO 通知によってデバイスが頻繁にウェイクアップされ、不必要にバッテリが消耗します。

コネクトスタンバイが有効になっている場合、デバイスはデバイスをウェイクアップするだけではなく、OS もウェイクアップするため、デバイスは os に通知しないようにする必要があります。 代わりに、モデムはデータ構造からすべての最新の PCO 要素をキャッシュし、OS がコネクトスタンバイ状態に出ると OS に通知します。 MBIM モデムの場合は、すべての PCO データ構造をキャッシュする必要があり、ホストがサブスクライブした後に PCO 通知を OS に送信するだけです。 これは、接続されたスタンバイを終了した後にシステム電源が電力に返されたときに、MBIM_CID_DEVICE_SERVICE_SUBSCRIBE_LIST CID を使用して行います。

## <a name="resetting-the-modem-based-on-pco-values"></a>PCO の値に基づいてモデムをリセットする

ネットワークから受信した PCO の値に基づいて、次のシナリオでモデムがリセットされます。

1.  ユーザーが PCO = 5 をネットワークから受信した後、自己ライセンス認証を完了しました。 新しい PCO 値 (3、0またはすべての携帯電話会社が認識可能なもの) が OS に送信され、OS から携帯電話会社のアプリに渡されます。
2.  PCO = 3 を受信した後、ユーザーがアカウントにクレジットを追加しました。 新しい PCO 値 (0、または任意の携帯電話会社が認識可能なもの) が OS に送信され、OS から携帯電話会社のアプリに渡されます。

ホストはリセットされているモデムを認識しないため、ホストからのアクティブな接続は非アクティブ化されず、リセット後に、モデムは自動的にこれらの PDN との接続を再確立する必要があります。 接続を確立し、ネットワークから新しい受信 PCO 値を受信すると、モデムは要請されていない[NDIS_STATUS_WWAN_PCO_STATUS](ndis-status-wwan-pco-status.md)通知をホストに提供します。

次の図は、これらのシナリオのいずれかが発生したときのモデムのリセットフローを示しています。この例では、Verizon ワイヤレスを例として使用しています。

![PCO 値に基づいた MB のモデムリセット](images/mb_PCO_modem_reset.png "PCO 値に基づいた MB のモデムリセット")

## <a name="ndis-interface-to-the-modem"></a>モデムへの NDIS インターフェイス

オペレータネットワークからモデムが受信した PCO 値の状態とペイロードを照会する方法については、「 [OID_WWAN_PCO](oid-wwan-pco.md)」を参照してください。 **OID_WWAN_PCO**は[**NDIS_WWAN_PCO_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pco_status)構造体を使用します。これには、ネットワークから pco 情報ペイロードを表す[**WWAN_PCO_VALUE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_pco_value)構造体が含まれています。

モデムのミニポートドライバーによって送信された状態通知については、モデムの現在の PCO 状態を OS に通知する方法については、「 [NDIS_STATUS_WWAN_PCO_STATUS](ndis-status-wwan-pco-status.md)」を参照してください。

## <a name="mb-cid-to-the-modem"></a>モデムに対する MB CID

サービス = **MBB_UUID_BASIC_CONNECT_EXT_CONSTANT**

サービス UUID = **3d01dcc5-fef5-4d05-0d3a-bef7058e9aaf**

PCO に対して次の Cid が定義されています。

| CID | コマンドコード | 最小 OS バージョン |
| --- | --- | --- |
| MBIM_CID_PCO | 9 | Windows 10 バージョン 1709 |

### <a name="mbim_cid_pco"></a>MBIM_CID_PCO

このコマンドは、携帯電話会社のネットワークからモデムでキャッシュされた PCO データを照会するために使用されます。

#### <a name="query"></a>クエリ

InformationBuffer には、唯一の関連フィールドが*SessionId*である**MBIM_PCO_VALUE**が含まれています。 *SessionId*は将来使用するために予約されており、Windows 10 バージョン1709では常に0になります。 クエリ内の*SessionId*は、どの IP データストリームの pco 値が関数によって返されるかを示します。 

#### <a name="set"></a>設定

適用できません。

#### <a name="unsolicited-event"></a>一方的なイベント

一方的なイベントには MBIM_PCO_VALUE が含まれ、アクティブ化された接続に新しい PCO 値が到着すると送信されます。

#### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 該当なし | MBIM_PCO_VALUE | 該当なし |
| 応答 | 該当なし | MBIM_PCO_VALUE | MBIM_PCO_VALUE |

#### <a name="data-structures"></a>データ構造

##### <a name="mbim_pco_type"></a>MBIM_PCO_TYPE

| 種類 | Value | 説明 |
| --- | --- | --- |
| MBIMPcoTypeComplete | 0 | 完全な PCO 構造体がネットワークから受信したとおりに渡されることを指定します。ヘッダーは、3GPP TS 24.008 仕様で定義されている PCO 構造体のオクテット3のプロトコルを現実に反映します。 |
| MBIMPcoTypePartial | 1 | モデムがネットワークから受信した PCO 構造のサブセットを渡すだけであることを指定します。 ヘッダーは 3GPP TS 24.008 仕様で定義されている PCO 構造に一致しますが、オクテット3の "構成プロトコル" が有効ではない可能性があります。 |

##### <a name="MBIM_PCO_TYPE"></a>MBIM-PCO-種類

| Offset | サイズ | フィールド | 型 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | セッション Id | UINT32 | クエリ内の SessionId は、どの IP データストリームの PCO 値が関数によって返されるかを示します。 |
| 4 | 4 | PcoDataSize | UINT32 | PcoData の長さ (0 ~ 256)。 クエリでは、この値は0になります。 |
| 8 | 4 | PcoDataType | UINT32 | PCO データ型。 詳細については、「 [MBIM_PCO_TYPE](#mbim_pco_type)」を参照してください。 |
| 12 | | PcoDataBuffer | DATABUFFER | 3GPP TS 24.008 spec の PCO 構造体。 |

#### <a name="status-codes"></a>状態コード

この CID は、一般的な状態コードのみを使用します。
