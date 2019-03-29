---
title: OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE
description: OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE は、IHV コンポーネントが関連要求を送信最近ピア デバイスにアソシエーションの応答を送信することを要求します。
ms.assetid: 8d19b009-db81-4b5e-ac63-5e6c5ad9727d
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 56732f65c9841acbe365267f46acd4ca0534d3c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582067"
---
# <a name="oidwditasksendapassociationresponse"></a>OID\_WDI\_タスク\_送信\_AP\_アソシエーション\_応答


OID\_WDI\_タスク\_送信\_AP\_アソシエーション\_IHV コンポーネントがアソシエーションに送信最近ピア デバイスにアソシエーションの応答を送信する応答の要求要求。

| オブジェクト | 中止できます。                                           | 既定の優先順位 (ホスト ドライバー ポリシー) | 通常の実行時間 (秒) |
|--------|---------------------------------------------------------|---------------------------------------|---------------------------------|
| ポート   | [はい]。 ポートは、中止した後、クリーンな状態でなければなりません。 | 3                                     | 1                               |

 

何らかの理由で、空のかどうか、送信が失敗[NDIS\_状態\_WDI\_INDICATION\_送信\_AP\_アソシエーション\_応答\_完全な](ndis-status-wdi-indication-send-ap-association-response-complete.md)正しい状態を設定されたヘッダーに含まれると、予想されます。

## <a name="task-parameters"></a>タスク パラメーター


| TLV                                                                                                      | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                      |
|----------------------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_アソシエーション\_応答\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/dn926137)      |                                |          | アソシエーションの応答のパラメーター。                                                                                 |
| [**WDI\_TLV\_ベンダー\_特定\_IE**](https://msdn.microsoft.com/library/windows/hardware/dn898076)                                |                                | x        | ポートは、アソシエーションの応答 IE ピア アダプターへの応答を送信する前に設定を追加する必要があります追加 IEs します。 |
| [**WDI\_TLV\_受信\_アソシエーション\_要求\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn926315) |                                |          | 受信の関連付け要求について説明します。                                                              |
| [**WDI\_TLV\_WFD\_アソシエーション\_状態**](https://msdn.microsoft.com/library/windows/hardware/mt269148)                        |                                | x        | 関連要求が拒否されたときに設定する状態値。                                                  |

 

## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_状態\_WDI\_INDICATION\_送信\_AP\_アソシエーション\_応答\_完了](ndis-status-wdi-indication-send-ap-association-response-complete.md)要件
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

 

 




