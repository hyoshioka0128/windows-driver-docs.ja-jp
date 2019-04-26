---
title: OID_WDI_TASK_SCAN
description: OID_WDI_TASK_SCAN は、BSS ネットワークのアンケートを要求します。 ポートは、IEEE 802.11 仕様の要件に従って、スキャンを実行します。
ms.assetid: c4131010-20f2-45a4-8fb9-5a1e3e9735e5
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_SCAN ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d7bf84cda2adbec918206cee5dfb3511cac1d75a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340023"
---
# <a name="oidwditaskscan"></a>OID\_WDI\_タスク\_スキャン


OID\_WDI\_タスク\_スキャン BSS ネットワークのアンケートを要求します。 ポートは、IEEE 802.11 仕様の要件に従って、スキャンを実行します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>オブジェクト</th>
<th>中止できます。</th>
<th>既定の優先順位 (ホスト ドライバー ポリシー)</th>
<th>通常の実行時間 (秒)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ポート</td>
<td>[はい]。 ポートは、中止した後、クリーンな状態でなければなりません。</td>
<td><p>6 (バック グラウンドのスキャン)</p>
<p>5 (ユーザーが開始したスキャン)</p></td>
<td>4</td>
</tr>
</tbody>
</table>

 

メッセージを格納しているタスクの開始、 [ **WDI\_TLV\_状態**](https://msdn.microsoft.com/library/windows/hardware/dn898068)ポートは、スキャンが開始され、その他のコマンドを受信する準備が後に示されます。

LiveUpdatesNeeded によって有効にすると、スキャンが開始されると、ポートが増分更新を提供する必要があります (の不要な兆候を使用して[NDIS\_状態\_WDI\_INDICATION\_BSS\_エントリ\_一覧](ndis-status-wdi-indication-bss-entry-list.md)) について、BSS エントリを検出します。 以前に検出されている必要があるが、現在のスキャンにポートが見つからなかった BSS エントリ ポートによって報告しません。 能力とパフォーマンスの理由から、ポートはスロットルがないと、3 つ以上検出された場合にのみ、または 3 より小さいエントリが検出がそれらを報告以上 500 ミリ秒のホストにない場合は、ホストに更新を送信する必要があります。 スキャンを完了すると、アダプターが BSS エントリを管理しない場合は後、は、検出された BSS エントリに注意してくださいその必要はありません。 スキャン操作が完了すると、ポートは、オペレーティング システムにタスクの完了通知を送信し、BSS エントリをホストに報告を停止する必要があります。 レガシ (Wi-Fi Direct ネットワーク) を検索するため、スキャン コマンドを使用し、ポート、プローブ要求に Wi-Fi Direct IEs を含める必要がありますいません。

アダプターが BSS エントリを管理しない場合は、ホストには、時間の期間でのスキャンからポートによって報告された BSS エントリが記録されています。 キャッシュされたエントリがタイムアウトし、それらをフラッシュします。 アダプターは、BSS エントリを管理している場合、キャッシュし、それらがタイムアウトになります。ホストが送信することがあります、 [OID\_WDI\_設定\_フラッシュ\_BSS\_エントリ](oid-wdi-set-flush-bss-entry.md)コマンドを明示的に、エントリを消去します。

ホストは、その BSSID を使用して BSS エントリを追跡します。 ポートは、同じ BSSID の 2 つの BSS エントリを報告する場合、ホストでは、別の 1 つが上書きされます。

スキャンが進行中は、ポートは (たとえば、インフラストラクチャまたは Wi-Fi Direct) は、既存の接続を維持する必要があります。 接続が既に存在する場合、ポート必要があります、一度にとサブセットの間のチャネルのサブセットをスキャン、メディアに他の接続アクセスを提供します。 ホストは、スキャン中に、アダプターのポートにパケットの送信要求を送信できます。

指定された BSS エントリでは、ポートはデバイスの特定のコンテキスト情報を含めることができます。 このコンテキスト情報は、その BSS エントリへの接続にポートが要求された場合、元のデバイスに渡されます。 ただし、このコンテキストが消去、ホストによって自動的に BSS エントリをフラッシュする場合。

スキャン コマンドを中止できます。 Abort コマンドを受信するには、新しい BSS ネットワークを検索して、できるだけ早くスキャン タスクを完了しようとしています。 ポートを停止する必要があります。 (通常または中止のため)、タスクが完了したら、ときに、そのポートで別のスキャンを実行できるように、ポートが正常な状態でなければなりません。

アダプター、スキャンを実行するときに規制の制限に違反する必要があります。

## <a name="task-parameters"></a>タスク パラメーター


| TLV                                                                       | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                                                                                                                                                                   |
|---------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_BSSID**](https://msdn.microsoft.com/library/windows/hardware/dn926153)                             |                                |          | ネットワークのスキャンする BSSID します。 このブロードキャストの MAC アドレスは、ステーションはすべて Bssid をスキャンします。                                                                                                                                                                                     |
| [**WDI\_TLV\_SSID**](https://msdn.microsoft.com/library/windows/hardware/dn898064)                               | x                              |          | ポートをスキャンする必要がある SSID リストの一覧。 この一覧で複数の Ssid 許可されるは、ワイルドカードは、それらのいずれか。 チャネルで作業中のスキャンを実施する際に、ポートは、一覧には、各 SSID のプローブ要求を送信する必要があります。 このリストが空の場合は、Ssid のすべてのポートをスキャンする必要があります。 |
| [**WDI\_TLV\_ベンダー\_特定\_IE**](https://msdn.microsoft.com/library/windows/hardware/dn898076) |                                | x        | ポートによって送信されたプローブ要求に含める必要がある 1 つまたは複数の i。 これらでは、パッシブ スキャンは使用されません。                                                                                                                                                                        |
| [**WDI\_TLV\_スキャン\_モード**](https://msdn.microsoft.com/library/windows/hardware/dn898052)                    |                                |          | モード パラメーターをスキャンします。                                                                                                                                                                                                                                                                         |
| [**WDI\_TLV\_スキャン\_熟考\_時間**](https://msdn.microsoft.com/library/windows/hardware/dn898051)       |                                |          | 時刻のパラメーターについて詳しく説明しません。                                                                                                                                                                                                                                                                        |
| [**WDI\_TLV\_バンド\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/dn926144)              | x                              | x        | スキャンすることをお勧めのチャネルのリスト。 最大スキャン時間の要件を満たしている限り、アダプターのサブセットまたはスーパー セットであるチャネルの一覧のスキャンを実行できます。 この一覧が空の場合、ポートがサポートされているすべてのチャネルでスキャンする必要があります。                                               |

 

## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_STATUS\_WDI\_INDICATION\_SCAN\_COMPLETE](ndis-status-wdi-indication-scan-complete.md)

## <a name="unsolicited-indication"></a>要請されていないを示す値

[NDIS\_STATUS\_WDI\_INDICATION\_BSS\_ENTRY\_LIST](ndis-status-wdi-indication-bss-entry-list.md)

デバイスはこの通知を使用して、BSS エントリが更新をホストに通知します。 これは、いつでも送信できます。

<a name="requirements"></a>要件
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

 

 




