---
title: WDI USB 中断シーケンス
description: NDIS がセレクティブ サスペンドのアイドル タイムアウト (SSIdleTimeout) よりも長時間アイドル状態が検出すると、UE は NDIS を呼び出します。
ms.assetid: EEDA274F-AC7D-4515-BAAF-FBEDDF95D2DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46c19fa7d9aab8224ad2fc992749694dcdc97967
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357095"
---
# <a name="wdi-usb-suspend-sequence"></a>WDI USB 中断シーケンス


NDIS 検出セレクティブ サスペンドのアイドル タイムアウトより長くアイドル状態にした場合 (*SSIdleTimeout*)、NDIS、UE を呼び出します。 NDIS を返すことによって、アイドル状態の通知を拒否することがあります、UE\_状態\_ビジーです。 UE と LE を呼び出す場合は、UE はアイドル状態の通知を拒否していない、 **LeIdleNotificationHander**、および、LE が拒否するか、そのまま使用します。

保留中のデータ、コマンド、またはデータや、LE までコマンドを送信する有効期限が切れる可能性がありますタイマーがない場合、UE はアイドル状態の通知を受け入れます。

WDI 受け取る D2 OID と、処理、OID が通常 d2 に切り替わりにある場合、WDI OID に設定する理由コードと共に送信する点を除いて**WDI\_設定\_POWER\_DX\_理由\_SELETIVE\_中断**します。

次のフロー図では、中断の順序を示します。

![wdi usb suspend sequence](images/wdi-usb-suspend-sequence-flow.png)

## <a name="related-topics"></a>関連トピック


[*MiniportWdiIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_idle_notification)

[**WDI\_TLV\_SET\_POWER\_DX\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-set-power-dx-reason)

 

 






