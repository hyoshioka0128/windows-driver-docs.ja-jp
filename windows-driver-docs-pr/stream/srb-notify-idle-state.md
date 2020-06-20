---
title: SRB \_ の \_ アイドル \_ 状態の通知
description: クラスドライバーは、最初の open 要求または最後の close 要求を送信する直前に、この要求をミニドライバーに送信します。 ミニドライバーは、 \_ \_ \_ USB セレクティブサスペンドから復帰するための通知として SRB NOTIFY IDLE 状態を使用できます。
ms.assetid: 7a2950a4-bd9f-4765-bb60-9e3aeeff49fb
keywords:
- ストリーミングメディアデバイスの SRB_NOTIFY_IDLE_STATE
topic_type:
- apiref
api_name:
- SRB_NOTIFY_IDLE_STATE
api_type:
- NA
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: 6d20d5db2658e6ce157ddca23d330b2fcbee24f9
ms.sourcegitcommit: f29360d62eb77b6ee875ce66483d5bc72785eede
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85111241"
---
# <a name="srb_notify_idle_state"></a>SRB \_ の \_ アイドル \_ 状態の通知

クラスドライバーは、最初の open 要求または最後の close 要求を送信する直前に、この要求をミニドライバーに送信します。 ミニドライバーは、 \_ \_ \_ [USB セレクティブサスペンド](../usbcon/usb-selective-suspend.md)から復帰するための通知として SRB NOTIFY IDLE 状態を使用できます。

## <a name="return-value"></a>戻り値

この要求は、通知パケットのみです。ミニドライバーが指定した戻り値は無視されます。

## <a name="remarks"></a>Remarks

SRB \_ 通知 \_ アイドル \_ 状態は、Microsoft Windows XP Service PACK 2 (SP2) 以降で送信されますが、microsoft windows Server 2003 では送信されません。

SRB \_ NOTIFY \_ IDLE \_ 状態は、Windows XP SP1 のストリームクラスドライバー (*Stream.sys*) に存在する、USB のセレクティブサスペンドの問題を修正します。 SRB \_ NOTIFY IDLE 状態を使用すると、 \_ \_ [stream クラス](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)と[USBCAMD2](https://docs.microsoft.com/windows-hardware/drivers/stream/usbcamd2-minidriver-operation)に基づいて、単一インスタンスミニドライバー内のセレクティブサスペンドをサポートできます。

Windows XP およびそれ以前のバージョンでは、SRB \_ NOTIFY \_ IDLE \_ 状態は存在しません。 Windows XP およびそれ以前のバージョンでは、ミニドライバーは[**SRB \_ GET \_ DEVICE \_ プロパティ**](srb-get-device-property.md)を受け取り、アイドル状態から復帰します。 次に、ミニドライバーは[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)を呼び出して、デバイスの状態を D0 に変更します。

Windows XP SP1 および Windows Server 2003 では、SRB \_ GET \_ DEVICE \_ プロパティはこのような状況では送信されません。 これらのオペレーティングシステムで*Stream.sys*を使用している場合は、前述のサポート技術情報の記事に記載されている手順に従ってください。

デバイスの最初のインスタンスを開くときに、クラスドライバーは \_ \_ \_ [**SRB \_ OPEN \_ device \_ インスタンス**](srb-open-device-instance.md)を送信する直前に SRB NOTIFY IDLE 状態を送信します。

デバイスの最後のインスタンスを閉じると、クラスドライバーは、 \_ \_ \_ デバイスから状態 D3 に遷移する要求を送信する直前に SRB NOTIFY IDLE 状態を送信します。

ストリームクラスドライバーが SRB NOTIFY IDLE STATE 要求を送信すると、 \_ \_ \_ ミニドライバーは[*Strminireceivedevicepacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)の呼び出しを受信します。

## <a name="see-also"></a>関連項目

[**SRB \_ GET \_ DEVICE \_ プロパティ**](srb-get-device-property.md)

[**SRB \_ 開いている \_ デバイス \_ インスタンス**](srb-open-device-instance.md)

[*StrMiniReceiveDevicePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)
