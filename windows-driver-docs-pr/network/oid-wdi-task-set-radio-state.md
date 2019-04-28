---
title: OID_WDI_TASK_SET_RADIO_STATE
description: OID_WDI_TASK_SET_RADIO_STATE は、アダプターの Wi-fi ラジオ状態の設定に使用されます。
ms.assetid: d7981df2-d3e5-49fd-8414-ca350775828b
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_SET_RADIO_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 93c39173824acf545f079d3cf83095a43ca4953e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365717"
---
# <a name="oidwditasksetradiostate"></a>OID\_WDI\_タスク\_設定\_ラジオ\_状態


OID\_WDI\_タスク\_設定\_ラジオ\_状態を使用して、アダプターの Wi-fi ラジオの状態を設定します。

| オブジェクト  | 中止できます。 | 既定の優先順位 (ホスト ドライバー ポリシー) | 通常の実行時間 (秒) |
|---------|---------------|---------------------------------------|---------------------------------|
| [アダプター] | X            | 1                                     | 1                               |

 

切断のアクティビティが完了した後にのみ、タスクを完了する必要があります。

IHV コンポーネントは、ホストに要請されていない問題ラジオ状態の変更を送信も可能性があります。

ホストは、無線をオフにして、前に、すべてのピアを切断しを実行しているグループの所有者を停止します。 アダプターは、無線 OFF または ON 遷移もステーション/移動プロファイルの情報を記憶する必要はありません。

## <a name="task-parameters"></a>タスク パラメーター


| TLV                                                                               | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                           |
|-----------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_ラジオ\_状態\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/dn898043) |                                |          | 無線の望ましい状態。 これは、1 に設定して、オプションが有効になっています。 0 に設定すると、オプションは無効になります。 |

 

## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_状態\_WDI\_INDICATION\_設定\_ラジオ\_状態\_完了](ndis-status-wdi-indication-set-radio-state-complete.md)
## <a name="unsolicited-indication"></a>要請されていないを示す値


[NDIS\_状態\_WDI\_INDICATION\_ラジオ\_状態](ndis-status-wdi-indication-radio-status.md)のアダプターのオプションの状態の変更をレポートにこのを示す値を使用します。 これは、アダプターによってハードウェア無線状態の変更が検出されたときとソフトウェア無線の変更は、ホストによってトリガーされたときに送信されます。

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

 

 




