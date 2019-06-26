---
title: OID_WDI_TASK_ROAM
description: OID_WDI_TASK_ROAM では、アダプターが、現在接続されているアクセス ポイントから新しい 1 つに移動しようとしたことを要求します。
ms.assetid: 22976d21-9212-4915-ab7a-fcc15d228db1
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_ROAM ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e72a78d92e4bece93c9ad26a7287667c4c13d27a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387229"
---
# <a name="oidwditaskroam"></a>OID\_WDI\_タスク\_ローミング


OID\_WDI\_タスク\_アダプターが、現在接続しているアジア太平洋から新しい 1 つに移動しようとしています。 移動要求。

| オブジェクト | 中止できます。                                                               | 既定の優先順位 (ホスト ドライバー ポリシー) | 通常の実行時間 (秒) |
|--------|-----------------------------------------------------------------------------|---------------------------------------|---------------------------------|
| ポート   | [はい]。 関連付けの解除後に中止されたため場合、dot11 リセットが続く必要があります。 | 4                                     | 10                              |

 

Microsoft コンポーネントは、アダプターは、移動の検討してください優先の BSS エントリの一覧を提供します。

このコマンドが発行されると、その現在関連付けられているのかどうか、アダプターは現在接続しているアジア太平洋関連付けを解除を新しい AP に移動しが必要です。 ここで古い AP の関連付けの解除を指定し、ap の関連付けの結果を示すし、タスクを完了します。

これは、ローミングを実行し、現在の AP に接続していないにも確認できます。 ここではなく関連付けまたは関連付け解除がないタスクが完了のみです。

スキャンとこのタスクの AP の選択の要件が場合と同じ[OID\_WDI\_タスク\_CONNECT](oid-wdi-task-connect.md)します。

## <a name="task-parameters"></a>タスク パラメーター


| TLV  | 許可されている複数の TLV インスタンス | 省略可能 | 説明 |
| --- | --- | --- | --- |
| [**WDI\_TLV\_CONNECT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-connect-parameters) |   |   | 接続パラメーター。 |  
| [**WDI\_TLV\_CONNECT\_BSS\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-connect-bss-entry)  | x  |   | 優先される候補の一覧は、BSS エントリを接続します。 ポートは、これら BSS エントリの一覧を使い果たすまでまたは接続が正常に完了しましたに接続しようとする必要があります。 ポートは、必要な場合、エントリを優先できます。 アダプターが接続 BSS 選択をオーバーライド ビットを設定した場合、許可/拒否リストの要件に従っている限り、この一覧にない BSS を選択できます。 | 

## <a name="task-completion-indication"></a>タスクの完了を示す値

[NDIS\_状態\_WDI\_INDICATION\_ローミング\_完了](ndis-status-wdi-indication-roam-complete.md)

## <a name="unsolicited-indications"></a>要請されていない問題

[NDIS\_状態\_WDI\_INDICATION\_アソシエーション\_結果](ndis-status-wdi-indication-association-result.md)

[NDIS\_状態\_WDI\_INDICATION\_関連付けの解除](ndis-status-wdi-indication-disassociation.md)

[NDIS\_状態\_WDI\_INDICATION\_FT\_ASSOC\_PARAMS\_が必要](ndis-status-wdi-indication-ft-assoc-params-needed.md)

[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)

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

 

 




