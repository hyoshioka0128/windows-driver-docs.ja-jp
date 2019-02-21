---
title: OID_WDI_TASK_DOT11_RESET
description: OID_WDI_TASK_DOT11_RESET は、IHV コンポーネントが指定されたポートで MAC および PHY の状態をリセットしていることを要求します。
ms.assetid: 5fcac1da-0776-47a5-87b7-8e831f968f7c
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_DOT11_RESET ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bc26d6c0100afb5836cf1f8b1e0cd61231abcfd8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532116"
---
# <a name="oidwditaskdot11reset"></a>OID\_WDI\_タスク\_DOT11\_リセット


OID\_WDI\_タスク\_DOT11\_リセットの要求、IHV コンポーネントが、指定されたポートで MAC および PHY 状態をリセットします。

| オブジェクト | 中止できます。 | 既定の優先順位 (ホスト ドライバー ポリシー) | 通常の実行時間 (秒) |
|--------|---------------|---------------------------------------|---------------------------------|
| ポート   | X            | 1                                     | 1                               |

 

Dot11 リセット コマンドを発行する前に、WDI ドライバーは IHV コンポーネントへの新しいコマンドの発行を停止し、ポート上で進行中のすべてのタスクを中止します。 また、Rx、TX キューをフラッシュします。

Dot11 リセットは、802.11 MLME と PLME リセット プリミティブのセマンティクスを組み合わせたものです。 IHV コンポーネントは、dot11 リセット要求を受信したときに、次のタスクを実行にする必要があります。

-   ポートの MAC のエンティティを初期状態にリセットします。
-   BSetDefaultMIB が true の場合、既定値に設定されているため、ポートの MIB 属性をリセットします。
-   PHY エンティティ用 Tx/rx ステート マシンをリセットし、フレームが送信されることを確認するだけに Rx 状態に設定します。
-   アダプターの受信キューをフラッシュし、送信キューでは、各パケットの送信を完了します。
-   [MAC アドレス] パラメーターが存在する場合は、指定された値、ポートの MAC アドレスをリセットします。
-   リセット操作の完了、dot11 前に、ポートの状態を INIT に設定します。

場合は、STA、AP、または Wi-Fi Direct クライアントまたは移動としてリセットされているポートが動作している、ホストが関連付けの解除をリセットする前に、ピアに送信する IHV コンポーネントを要求するタスクを切断をトリガーしたとします。 そのため、IHV コンポーネントは、再度実行する必要はありません。

## <a name="task-parameters"></a>タスク パラメーター


| TLV                                                                               | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                       |
|-----------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------|
| [**WDI\_TLV\_DOT11\_リセット\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/dn926302) |                                |          | Dot11 リセットのパラメーターです。                   |
| [**WDI\_TLV\_構成済み\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926257) |                                | X        | MAC アドレス、ポートに使用する必要があります。 |

 

## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_状態\_WDI\_INDICATION\_DOT11\_リセット\_完了](ndis-status-wdi-indication-dot11-reset-complete.md)要件
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

 

 




