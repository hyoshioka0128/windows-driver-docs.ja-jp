---
title: I2C を使用した子デバイスとの通信
description: I2C を使用した子デバイスとの通信
ms.assetid: 5eea2257-49ca-4d76-a6a1-91401595750f
keywords:
- I2C WDK ビデオのミニポート
- ビデオのミニポート ドライバー WDK Windows 2000 では、子デバイス
- 子デバイス WDK ビデオのミニポート、I2C を使用して通信するには
- ビデオのミニポート ドライバー WDK Windows 2000、I2C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e8c0cdb4eaff53afe057cb85f2adea6ce4c48ff
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370614"
---
# <a name="using-i2c-to-communicate-with-a-child-device"></a>I2C を使用した子デバイスとの通信


## <span id="ddk_using_i2c_to_communicate_with_a_child_device_gg"></span><span id="DDK_USING_I2C_TO_COMMUNICATE_WITH_A_CHILD_DEVICE_GG"></span>


Microsoft Windows xp 以降、プラグ アンド プレイ マネージャがビデオ アダプターの子のデバイスを列挙した後、ミニポート ドライバーできますデバイスと通信、アダプターの子で、 *I2C*バス I²C プロトコルを使用します。 ミニポート ドライバーによって公開されているソフトウェア インターフェイスを使用して、ミニポート ドライバーと WDM ドライバー I²C バス上のそれらのデバイスの間の通信が行われる (」の説明に従って[子デバイスのドライバーとの通信](communicating-with-the-driver-of-a-child-device.md))。 ミニポート ドライバーでは、それらのビデオ ポート ドライバーによって公開される、新しいハードウェア インターフェイスを使用して I²C バス上のデバイス間の物理的な通信を開始できます。 ビデオ ポート ドライバーのによって提供されるハードウェア I²C インターフェイスを使用できます、ミニポート ドライバーからの読み取りまたは I²C バス経由で子の物理デバイスに書き込みを I²C マスター デバイス (通常は、グラフィックス チップ) 場合は、 [ **VideoPortQueryServices** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportqueryservices)ルーチン。 I²C バス経由でこの通信が同じ I²C バス上のハードウェア デバイスに厳密に制限されることに注意してください。 ミニポート ドライバーの作成者は、このようなすべての通信にこれらのルーチンを使用する、強くお勧めします。

このモードでの通信もビデオ アダプターがコンポーネントを WDM ドライバーがない場合に役立ちます。 たとえば、ビデオ アダプターには、ドーター ボードまたはデジタルのフラット パネルにあるビデオ画像を送信するために使用する回線があります。 この場合、ミニポート ドライバーと、によって提供されるハードウェア I²C インターフェイスの使用**VideoPortQueryServices** I²C バス経由でその回線にコマンドを送信します。

![回線 (i2c) の間の統合インターフェイスを使用して子デバイスとの通信を示す図](images/i2cfig1.png)

上記の図は、ミニポート ドライバーが I²C バス上の 2 つのハードウェア デバイス間の通信を開始する方法を示しています。

ビデオ ポートの I²C ルーチンを利用するには、ミニポート ドライバーはクエリの I²C インターフェイスのビデオ ポート ドライバーを実行する必要があります。 この準備として、ミニポート ドライバーを割り当てる必要があります、 [**ビデオ\_ポート\_I2C\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_port_i2c_interface)構造体、およびその最初の 2 つのメンバーを初期化 (、**サイズ**と**バージョン**メンバー) に適切な値。 ミニポート ドライバーを呼び出して、ビデオ ポート ドライバーの[ **VideoPortQueryServices** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportqueryservices)ルーチン、設定、 *servicesType*パラメーターを**VideoPortServicesI2C**、および設定、 *pInterface*パラメーターを部分的に初期化ビデオ\_ポート\_I2C\_インターフェイス構造体。

場合に呼び出し**VideoPortQueryServices**が成功すると、ビデオの残りのメンバーでのビデオ ポート ドライバーが\_ポート\_I2C\_インターフェイス構造体、4 つのアドレスを含むI²C ルーチン:[**I2CStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pi2c_start)、 [ **I2CStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pi2c_stop)、 [ **I2CRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pi2c_read)、および[ **I2CWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pi2c_write).

*I2CStart*と*I2CStop* 、それぞれ子デバイスとの通信を開始して使用との通信を終了します。

*I2CRead*子デバイスから、指定したバイト数を読み取ります*I2CWrite*指定したバイト数を書き込みます。

 

 





