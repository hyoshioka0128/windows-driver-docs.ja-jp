---
title: WDI USB 中断シーケンス
description: NDIS がセレクティブサスペンドアイドルタイムアウト (SSIdleTimeout) を超えるアイドル状態を検出すると、NDIS は UE-V を呼び出します。
ms.assetid: EEDA274F-AC7D-4515-BAAF-FBEDDF95D2DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 414a7b54feb02498e6615d0bfebecb8f91f916f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841710"
---
# <a name="wdi-usb-suspend-sequence"></a>WDI USB 中断シーケンス


NDIS がセレクティブサスペンドアイドルタイムアウト (*Ssidletimeout*) を超えるアイドル状態を検出すると、NDIS は ue-v を呼び出します。 この場合、NDIS\_ステータス\_ビジー状態を返すことによって、アイドル状態の通知が拒否されることがあります。 UE-V がアイドル通知を拒否していない場合、UE-V は**LeIdleNotificationHander**を使用して le を呼び出し、le は拒否または同意することがあります。

データまたはコマンドを LE に送信するために期限切れになる可能性がある保留中のデータ、コマンド、タイマーがない場合、UE-V はアイドル状態の通知を受け取ります。

WDI が D2 OID を受け取ると、OID は通常の D2 のように処理されますが、理由コードが\_WDI に設定された WDI OID **\_\_DX\_reason\_SELETIVE\_SUSPEND を設定**して送信される点が異なります。

次のフロー図は、中断シーケンスを示しています。

![wdi usb 中断シーケンス](images/wdi-usb-suspend-sequence-flow.png)

## <a name="related-topics"></a>関連トピック


[*MiniportWdiIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_idle_notification)

[**WDI\_TLV\_設定\_電源\_DX\_理由**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-set-power-dx-reason)

 

 






