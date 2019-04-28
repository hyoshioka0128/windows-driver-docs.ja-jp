---
title: SRB\_通知\_IDLE\_状態
description: クラス ドライバーは、最初のオープン要求または閉じる最後の要求を送信する前に、すぐに、ミニドライバーにこの要求を送信します。 SRB を使用できるようにミニドライバー\_通知\_IDLE\_USB セレクティブ サスペンドからの復帰への通知と状態。
ms.assetid: 7a2950a4-bd9f-4765-bb60-9e3aeeff49fb
keywords:
- SRB_NOTIFY_IDLE_STATE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_NOTIFY_IDLE_STATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8532033ea5d2988db5ebb212efc5a31bcd75115f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379946"
---
# <a name="srbnotifyidlestate"></a>SRB\_通知\_IDLE\_状態


クラス ドライバーは、最初のオープン要求または閉じる最後の要求を送信する前に、すぐに、ミニドライバーにこの要求を送信します。 SRB を使用できるようにミニドライバー\_通知\_IDLE\_状態から復帰への通知として[USB のセレクティブ サスペンド](../usbcon/usb-selective-suspend.md)します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

この要求が通知パケットだけです。ミニドライバーが指定した戻り値は無視されます。

<a name="remarks"></a>注釈
-------

SRB\_通知\_IDLE\_Microsoft Windows Server 2003 ではなく Microsoft Windows XP Service Pack 2 (SP2) 以降に状態が送信されます。

SRB\_通知\_IDLE\_状態の修正、USB のセレクティブ サスペンド ストリーム クラス ドライバー内に存在する問題 (*Stream.sys*) で説明されている Windows XP SP1 で[ナレッジ記事 813348](https://go.microsoft.com/fwlink/p/?linkid=210855)します。 SRB を使用する\_通知\_IDLE\_に基づいて 1 つのインスタンスのミニドライバー内で選択的にサポートするために状態が一時中断[クラスのストリーム](https://msdn.microsoft.com/library/windows/hardware/ff568277)と[USBCAMD2](https://msdn.microsoft.com/library/windows/hardware/ff568573)します。

Windows XP 以降では、SRB\_通知\_IDLE\_状態は存在しません。 Windows xp 以降、ミニドライバーを受け取る[ **SRB\_取得\_デバイス\_プロパティ**](srb-get-device-property.md)がアイドル状態からスリープ解除します。 ミニドライバーを呼び出して[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734) D0 にデバイスの状態を変更します。

Windows XP SP1、および Windows Server 2003、SRB で\_取得\_デバイス\_プロパティは、このような状況では送信されません。 使用する場合*Stream.sys*これらのオペレーティング システムでは、前述のサポート技術情報記事の手順に従います。

クラスのドライバーが SRB を送信して、デバイスの最初のインスタンスを開くときに\_通知\_IDLE\_状態を送信する前に、すぐに[ **SRB\_オープン\_デバイス\_インスタンス**](srb-open-device-instance.md)します。

クラスのドライバーが SRB を送信して、デバイスの最後のインスタンスを閉じるときに\_通知\_IDLE\_D3 の状態に遷移するデバイスの要求を送信する前に、すぐに状態。

ストリーム クラスのドライバーが、SRB を送信すると\_通知\_IDLE\_状態が要求への呼び出しを受け取るようにミニドライバー [ *StrMiniReceiveDevicePacket*](https://msdn.microsoft.com/library/windows/hardware/ff568463)します。

## <a name="see-also"></a>関連項目


[**SRB\_取得\_デバイス\_プロパティ**](srb-get-device-property.md)

[**SRB\_オープン\_デバイス\_インスタンス**](srb-open-device-instance.md)

[*StrMiniReceiveDevicePacket*](https://msdn.microsoft.com/library/windows/hardware/ff568463)

 

 






