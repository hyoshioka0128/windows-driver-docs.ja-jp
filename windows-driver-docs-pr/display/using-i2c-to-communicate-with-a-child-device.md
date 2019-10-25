---
title: I2C を使用した子デバイスとの通信
description: I2C を使用した子デバイスとの通信
ms.assetid: 5eea2257-49ca-4d76-a6a1-91401595750f
keywords:
- I2C WDK ビデオミニポート
- ビデオミニポートドライバー WDK Windows 2000、子デバイス
- 子デバイス WDK ビデオミニポート、I2C を使用した通信
- ビデオミニポートドライバー WDK Windows 2000、I2C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d1d016d337519b24cba0e9dbdddda0e8939eec4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829259"
---
# <a name="using-i2c-to-communicate-with-a-child-device"></a>I2C を使用した子デバイスとの通信


## <span id="ddk_using_i2c_to_communicate_with_a_child_device_gg"></span><span id="DDK_USING_I2C_TO_COMMUNICATE_WITH_A_CHILD_DEVICE_GG"></span>


Microsoft Windows XP 以降では、プラグアンドプレイマネージャーがビデオアダプターの子デバイスを列挙した後、ミニポートドライバーは、I ² C プロトコルを使用して、 *I2C*バス上のアダプターの子デバイスと通信できます。 I ² C バス上のこれらのデバイスのミニポートドライバーと WDM ドライバーの間の通信は、ミニポートドライバーによって公開されているソフトウェアインターフェイス (「[子デバイスのドライバーとの通信](communicating-with-the-driver-of-a-child-device.md)」を参照) によって発生する可能性があります。 ミニポートドライバーは、ビデオポートドライバーによって公開されている新しいハードウェアインターフェイスを使用して、I ² C バス上のデバイス間の物理的な通信を開始できます。 ミニポートドライバーが i ² C バスを介して物理的な子デバイスの読み取りまたは書き込みを行うために I ² C マスターデバイス (通常はグラフィックスチップ) を必要とする場合は、ビデオポートドライバーの[**Videoportqueryservices**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportqueryservices)ルーチンによって提供されるハードウェア i ² c インターフェイスを使用できます。 I ² C バスを介したこの通信は、同じ I ² C バス上のハードウェアデバイスのみに制限されていることに注意してください。 ミニポートドライバーの作成者は、これらのルーチンをすべての通信に使用することを強くお勧めします。

この通信モードは、WDM ドライバーがないコンポーネントがビデオアダプターに含まれている場合にも役立ちます。 たとえば、ビデオアダプターには、ビデオイメージをデジタルフラットパネルに送信するために使用される1つのボードまたは回線がある場合があります。 この場合、ミニポートドライバーは、 **Videoportqueryservices**によって提供されるハードウェア I ² c インターフェイスを使用して、i ² c バス経由でその回路にコマンドを送信できます。

![統合回線 (i2c) インターフェイスを介して子デバイスと通信する方法を示す図](images/i2cfig1.png)

上の図は、ミニポートドライバーが I ² C バス上の2つのハードウェアデバイス間の通信を開始する方法を示しています。

ビデオポートの I ² C ルーチンを活用するために、ミニポートドライバーは、ビデオポートドライバーで I ² C インターフェイスを照会する必要があります。 このための準備として、ミニポートドライバーは、 [**I2C\_インターフェイス構造\_のビデオ\_ポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_port_i2c_interface)を割り当て、最初の2つのメンバー (**サイズ**と**バージョン**のメンバー) を適切な値に初期化する必要があります。 次に、ミニポートドライバーはビデオポートドライバーの[**Videoportqueryservices**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportqueryservices)ルーチンを呼び出し、 *Servicestype*パラメーターを**VideoPortServicesI2C**に設定し、 *pinterface*パラメーターを部分的に初期化されたに設定します。VIDEO\_PORT\_I2C\_インターフェイス構造です。

**Videoportqueryservices**の呼び出しが成功した場合、ビデオポートドライバーは、次の4つの I ² C ルーチンのアドレスを[**含む、video**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pi2c_start)\_ポート\_I2C\_インターフェイス構造の残りのメンバーを入力します。 [**I2CStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pi2c_stop)、 [**I2CRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pi2c_read)、および[**I2CWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pi2c_write)。

*I2CStart*と*I2CStop*はそれぞれ、子デバイスとの通信を開始し、そのデバイスとの通信を終了するために使用されます。

*I2CRead*は、子デバイスから指定されたバイト数を読み取ります。*I2CWrite*は、指定されたバイト数をそれに書き込みます。

 

 





