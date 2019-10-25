---
title: IEEE 1394 ドライバー スタック
description: IEEE 1394 ドライバー スタック
ms.assetid: 3c8c218e-d814-451c-9a39-fe7fe5fb7aaf
keywords:
- IEEE 1394 WDK バス、ドライバースタック
- 1394 WDK バス、ドライバースタック
- ドライバースタック WDK IEEE 1394 バス
- スタック WDK IEEE 1394 バス
- デバイススタック WDK IEEE 1394 バス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b550fd58d087ffd5d6fef79dac14e77e5df7d65
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841524"
---
# <a name="the-ieee-1394-driver-stack"></a>IEEE 1394 ドライバー スタック





次の図は、新しい 1394 bus ドライバーと Microsoft がサポートしている1394クライアントドライバーを使用した IEEE 1394 ドライバースタックを示しています。

![ieee 1394 ドライバースタックを示す図](images/1394driverstack.png)

Ieee 1394 バスドライバーに接続するデバイスのクライアントドライバーは、IEEE 1394 ドライバースタックの上にあります。 バスドライバーは、ハードウェアに依存しない、IEEE 1394 バスに対するインターフェイスを提供します。 デバイスドライバーは、IEEE 1394 バスドライバーによって処理される Irp を送信することによって、デバイスと通信します。 Windows 7 より前では、バスドライバーは、マザーボードのホストコントローラー (ochi1394) のポートドライバー (1394bus とプライマリミニポートドライバーを組み合わせたものでした。 Windows 7 以降のバージョンでは、レガシポート/ミニポートバスドライバーは、カーネルモードドライバーフレームワーク (KMDF) を使用して実装されたモノリシック IEEE 1394 バスドライバーである1394ohci に置き換えられています。 1394ohci バスドライバーは、レガシ1394バスドライバーと完全に下位互換性があります。 新しいバスドライバーとレガシ1394バスドライバーの動作の既知の相違点の詳細については、「 [Windows 7 の IEEE 1394 バスドライバー](https://docs.microsoft.com/windows-hardware/drivers/ieee/IEEE-1394-Bus-Driver-in-Windows-7)」を参照してください。

次の図は、レガシーと新しい1394バスドライバーの関係を示しています。

![レガシーと新しい1394バスドライバーの関係を示す図。](images/1394busdriver.png)

バスに接続されているデバイスに対してコマンドを発行するために、ドライバーは irp [ **\_MJ\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)コード[**IOCTL\_1394\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ni-1394-ioctl_1394_class)を使用して irp を発行します。 このドライバーは、IEEE 1394 i/o request block ([**IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_irb)) のパラメーターをパッケージ化し、そのパラメーターへのポインターを、IRP の**引数 1**メンバーに渡します。 IRB の**Functionnumber**メンバーによって操作の種類が決定され、 **u**メンバーによって操作が記述されます。 バスドライバーは IOCTL\_1394\_クラスの IRP を使用して、バスとホストコントローラーの両方にインターフェイスを提供します。

IRB 構造体には、各バス要求と要求固有のパラメーターに適用されるパラメーターが含まれています。 IRB の**u**メンバーには、要求固有のパラメーターが含まれています。これは、データ構造体の和集合で、要求の種類ごとに1つです。

通常の操作中、ドライバーは通常の i/o 要求 ( [**IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)など) を受信し、適切な IEEE 1394 操作に変換し、IOCTL\_1394\_クラスを介してその操作をデバイスにディスパッチします。

## <a name="related-topics"></a>関連トピック
[Windows 7 の IEEE 1394 バスドライバー](https://docs.microsoft.com/windows-hardware/drivers/ieee/IEEE-1394-Bus-Driver-in-Windows-7)  



