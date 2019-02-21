---
title: WDI USB シーケンスを中断します。
description: NDIS がセレクティブ サスペンドのアイドル タイムアウト (SSIdleTimeout) よりも長時間アイドル状態が検出すると、UE は NDIS を呼び出します。
ms.assetid: EEDA274F-AC7D-4515-BAAF-FBEDDF95D2DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 126e031d53aeac5190a5785948a648ab1f41a3f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553500"
---
# <a name="wdi-usb-suspend-sequence"></a>WDI USB シーケンスを中断します。


NDIS 検出セレクティブ サスペンドのアイドル タイムアウトより長くアイドル状態にした場合 (*SSIdleTimeout*)、NDIS、UE を呼び出します。 NDIS を返すことによって、アイドル状態の通知を拒否することがあります、UE\_状態\_ビジーです。 UE と LE を呼び出す場合は、UE はアイドル状態の通知を拒否していない、 **LeIdleNotificationHander**、および、LE が拒否するか、そのまま使用します。

保留中のデータ、コマンド、またはデータや、LE までコマンドを送信する有効期限が切れる可能性がありますタイマーがない場合、UE はアイドル状態の通知を受け入れます。

WDI 受け取る D2 OID と、処理、OID が通常 d2 に切り替わりにある場合、WDI OID に設定する理由コードと共に送信する点を除いて**WDI\_設定\_POWER\_DX\_理由\_SELETIVE\_中断**します。

次のフロー図では、中断の順序を示します。

![wdi usb suspend sequence](images/wdi-usb-suspend-sequence-flow.png)

## <a name="related-topics"></a>関連トピック


[*MiniportWdiIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/mt297563)

[**WDI\_TLV\_SET\_POWER\_DX\_REASON**](https://msdn.microsoft.com/library/windows/hardware/dn898060)

 

 






