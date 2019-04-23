---
title: OID_WDI_SET_P2P_LISTEN_STATE
description: OID_WDI_SET_P2P_LISTEN_STATE は、ポートで、Wi-Fi Direct リッスン状態を設定します。
ms.assetid: d488903b-ef64-44b6-b07a-70168a0ccfd8
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_P2P_LISTEN_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 28f73e6b10ae13999c82869f3eddcc9af936c7b1
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903518"
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
| [**WDI\_TLV\_P2P\_リッスン\_状態**](https://msdn.microsoft.com/library/windows/hardware/dn897975)       |                                |          | 必要なリッスン状態です。                                                                                                                                            |
| [**WDI\_TLV\_P2P\_チャネル\_数**](https://msdn.microsoft.com/library/windows/hardware/dn897869)   |                                | x        | ホストの必要なリッスン チャネル Wi-Fi Direct を有効にする場合は、状態をリッスンします。 このオプションが指定されていない場合、ポートは単独でリッスン チャネルを選択できます。 |
| [**WDI\_TLV\_P2P\_リッスン\_期間**](https://msdn.microsoft.com/library/windows/hardware/dn897973) |                                |          | サイクル期間と待機時間。                                                                                                                                  |

 

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

 

 




