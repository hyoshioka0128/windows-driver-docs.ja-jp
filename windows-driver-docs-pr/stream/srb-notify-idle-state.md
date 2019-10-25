---
title: SRB\_\_アイドル状態の\_状態に通知
description: クラスドライバーは、最初の open 要求または最後の close 要求を送信する直前に、この要求をミニドライバーに送信します。 ミニドライバーは、SRB を使用して、USB セレクティブサスペンドからの復帰を通知として\_アイドル状態の\_を通知\_ことができます。
ms.assetid: 7a2950a4-bd9f-4765-bb60-9e3aeeff49fb
keywords:
- SRB_NOTIFY_IDLE_STATE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- SRB_NOTIFY_IDLE_STATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c9b85da8423269f8761a00e8ed2402cf7d41815
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843293"
---
# <a name="srb_notify_idle_state"></a>SRB\_\_アイドル状態の\_状態に通知


クラスドライバーは、最初の open 要求または最後の close 要求を送信する直前に、この要求をミニドライバーに送信します。 ミニドライバーは、SRB を使用して、 [USB セレクティブサスペンド](../usbcon/usb-selective-suspend.md)からの復帰を通知として\_アイドル状態の\_を通知\_ことができます。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

この要求は、通知パケットのみです。ミニドライバーが指定した戻り値は無視されます。

<a name="remarks"></a>注釈
-------

SRB\_NOTIFY\_IDLE\_状態は、microsoft Windows XP Service Pack 2 (SP2) 以降で送信されますが、Microsoft Windows Server 2003 では送信されません。

SRB\_通知\_アイドル\_状態は、[サポート技術情報の記事 813348](https://go.microsoft.com/fwlink/p/?linkid=210855)に記載されている WINDOWS XP SP1*のストリームクラスドライバー (* ) に存在する、USB のセレクティブサスペンドの問題を修正します。 \_SRB を使用して\_アイドル状態の\_状態を通知し、[ストリームクラス](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)と[USBCAMD2](https://docs.microsoft.com/windows-hardware/drivers/stream/usbcamd2-minidriver-operation)に基づいて単一インスタンスのミニドライバー内でセレクティブサスペンドをサポートすることができます。

Windows XP およびそれ以前のバージョンでは、SRB\_NOTIFY\_IDLE\_状態は存在しません。 Windows XP およびそれ以前のバージョンでは、ミニドライバーは[**SRB\_GET\_DEVICE\_プロパティ**](srb-get-device-property.md)を受け取り、アイドル状態から復帰します。 次に、ミニドライバーは[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)を呼び出して、デバイスの状態を D0 に変更します。

Windows XP SP1 および Windows Server 2003 では、このような状況では、SRB\_GET\_DEVICE\_プロパティは送信されません。 これらのオペレーティングシステムで *.sys*を使用する場合は、前述のサポート技術情報の記事に記載されている手順に従ってください。

デバイスの最初のインスタンスを開くときに、クラスドライバーは\_SRB を送信し、 [**SRB\_OPEN\_device\_インスタンス**](srb-open-device-instance.md)を送信する直前に\_アイドル状態の\_状態を通知します。

デバイスの最後のインスタンスを閉じると、クラスドライバーは、デバイスから状態 D3 に移行するように要求を送信する直前に、SRB\_通知\_アイドル状態の\_状態に送信します。

ストリームクラスドライバーが\_\_アイドル状態の\_状態要求を送信すると、ミニドライバーは[*Strminireceivedevicepacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)の呼び出しを受信します。

## <a name="see-also"></a>関連項目


[**SRB\_GET\_DEVICE\_プロパティ**](srb-get-device-property.md)

[**SRB\_開いているデバイス\_インスタンス\_** ](srb-open-device-instance.md)

[*StrMiniReceiveDevicePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)

 

 






