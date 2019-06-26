---
title: OID_WDI_SET_P2P_LISTEN_STATE
description: OID_WDI_SET_P2P_LISTEN_STATE は、ポートで、Wi-Fi Direct リッスン状態を設定します。
ms.assetid: d488903b-ef64-44b6-b07a-70168a0ccfd8
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_P2P_LISTEN_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 0f4d5ad2beb345db52457b05071a71c61ef1304f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359194"
---
# <a name="oidwdisetp2plistenstate"></a>OID\_WDI\_設定\_P2P\_リッスン\_状態


OID\_WDI\_設定\_P2P\_リッスン\_状態は、ポートで、Wi-Fi Direct リッスン状態を設定します。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

リッスン状態では、さまざまなレベルがあるし、ポートはポート間の同時実行制御の要件に準拠する予定です。

このプロパティでは、仮想化されたアダプターのポートを Wi-Fi Direct インターフェイスに適用できるのみです。

リッスン状態がアクティブの場合、ポートが無線をソーシャル チャンネルで一定期間保管するに必要です。

アダプターが非ソーシャル チャンネルで動作している仮想化されたポートで、ポートがそのチャネル上で検出なる可能性があります。 この動作を使用する場合、ポートは Wi-Fi Direct 検出のスキャン フェーズで迅速に検出するには、他のアダプターを許可する非常に高可用性である必要があります。 これは、チャネルは、低待機時間シナリオでホッピングを回避するために、トレードオフとして提供されます。

**注**  このプロパティは、他のプロパティまたはポートに発行されたタスクとの競合を引き起こす可能性のあるポートにラジオ時間スライスの要件を指定します。

 

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                         | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                                      |
|-----------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_リッスン\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-listen-state)       |                                |          | 必要なリッスン状態です。                                                                                                                                            |
| [**WDI\_TLV\_P2P\_チャネル\_数**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-channel-number)   |                                | x        | ホストの必要なリッスン チャネル Wi-Fi Direct を有効にする場合は、状態をリッスンします。 このオプションが指定されていない場合、ポートは単独でリッスン チャネルを選択できます。 |
| [**WDI\_TLV\_P2P\_リッスン\_期間**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-listen-duration) |                                |          | サイクル期間と待機時間。                                                                                                                                  |

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加データがありません。 ヘッダー内のデータで十分です。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




