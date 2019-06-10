---
title: KMDF ドライバーのサンプル
description: このトピックでは、Windows デベロッパー センター - ハードウェアからダウンロード可能なカーネル モード ドライバー フレームワーク (KMDF) サンプル ドライバーを使用します。
ms.assetid: 83d15b96-63b1-4584-8ef4-ccbdcc1522bb
keywords:
- カーネル モード ドライバー WDK KMDF、サンプル
- KMDF WDK サンプル ドライバー
- カーネル モード ドライバー フレームワーク開発の WDK サンプル ドライバー
- フレームワーク ベースのドライバー WDK KMDF、サンプル
- WDK KMDF ドライバーをサンプルします。
ms.date: 06/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: ae5b17e143aa3db86f410df40c130337065ff8bc
ms.sourcegitcommit: 2589492f3c14f779efa8b446e81d4e0f6d048f4f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2019
ms.locfileid: "66815091"
---
# <a name="sample-kmdf-drivers"></a>KMDF ドライバーのサンプル


このトピックでは、カーネル モード ドライバー フレームワーク (KMDF) サンプル ドライバーからダウンロードできる、 [Windows ドライバーのサンプル リポジトリ](https://github.com/Microsoft/Windows-driver-samples)GitHub でします。




サンプルのビルド方法の詳細については、次を参照してください。[ドライバーをビルド](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)します。

<a href="" id="echo"></a>ECHO では、フレームワークのキューおよび要求オブジェクトと自動同期を使用する方法を示します。

このサンプルの詳細については、次を参照してください。、 [KMDF Echo サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/echo/kmdf)します。

<a href="" id="fakemodem"></a>モデム AT コマンド送受信するドライバーの単純なコント ローラーなし FakeModem を示します。

このサンプルの詳細については、次を参照してください。、 [Fakemodem ドライバー](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/modem/fakemodem)します。

<a href="" id="firefly"></a>FIREFLY デモの人間をプログラミングでは、I/O 制御コード (Ioctl) を使用してデバイス (HID) デバイスを入力し、Windows Management Instrumentation (WMI) インターフェイスを提供します。

このサンプルの詳細については、次を参照してください。、 [FIREFLY - HID デバイスのフィルター ドライバーを WDF](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/firefly)します。

<a href="" id="hidusbfx2"></a>HIDUSBFX2 は HID デバイス用のミニドライバーを作成する方法と、HID デバイスを非-HID USB デバイスをマップする方法について説明します。 デバイスは、OSR usb-fx2 Learning Kit に含まれます。

このサンプルの詳細については、次を参照してください。 [HIDUSBFX2](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/hidusbfx2)します。

<a href="" id="kbfiltr"></a>KbFiltr では、ps/2 キーボードの上のデバイス フィルター ドライバーを示します。

このサンプルの詳細については、次を参照してください。、[キーボード入力 WDF フィルター ドライバー (Kbfiltr)](https://github.com/Microsoft/Windows-driver-samples/tree/master/input/kbfiltr)します。

<a href="" id="ndisprot"></a>NDISProt は、NDIS 5.0 または 5.1 および NDIS 6.0 のコネクションレス プロトコル ドライバーを示します。

このサンプルの詳細については、次を参照してください。 [NDISProt コネクションレス WDF プロトコル](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/ndis/ndisprot_kmdf)します。

<a href="" id="nonpnp"></a>非 PNP は、フレームワークを使用する非プラグ アンド プレイ (PnP) ドライバーを示します。

このサンプルの詳細については、次を参照してください。[非 PNP](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/ioctl/kmdf)します。

<a href="" id="kmdf-fx2"></a>KMDF\_FX2 が一括で行って、OSR usb-fx2 Learning Kit に含まれている USB デバイスへのデータ転送を中断する方法を示します。

このサンプルの詳細については、次を参照してください。 [kmdf\_fx2](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/kmdf_fx2)します。

<a href="" id="pcidrv"></a>PCIDRV 完全に機能フレームワーク ベースのドライバー Intel 82557/82558 PCI Ethernet アダプター (10/100) と Intel 互換の。

このサンプルの詳細については、次を参照してください。、 [PCIDRV - PCI デバイスのドライバーを WDF](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/pcidrv)します。

<a href="" id="plx9x5x"></a>PLX9x5x では、DMA をサポートし、PLX9656/9653RDK LITE のボードを使用する汎用 PCI デバイス用のドライバーを記述する方法を示します。

このサンプルの詳細については、次を参照してください。、 [PLX9x5x PCI ドライバ](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/PLX9x5x)します。

<a href="" id="serial"></a>シリアル WDM シリアル サンプル ドライバーに基づいているフレームワークに基づくシリアル ドライバー。

このサンプルの詳細については、次を参照してください。、[シリアル サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serial)します。

<a href="" id="toaster"></a>WDM トースター サンプル ドライバーのトースター Framework ベースのバージョン。 トースター サンプルには、フィルター ドライバー、関数ドライバー、および 1 つのドライバー スタックを作成するバス ドライバーが含まれています。 このサンプルでは、通信にはドライバー スタックとリモートの I/O ターゲットを使用する追加のカーネル モード ドライバーも含まれます。

このサンプルの詳細については、次を参照してください。[トースター](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster/toastDrv)します。

<a href="" id="usbsamp"></a>UsbSamp では、フレームワークを使用して、USB デバイスへの一括と isochronous データ転送を実行する方法を示します。

このサンプルの詳細については、次を参照してください。、 [Usbsamp サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/usbsamp)します。

<a href="" id="wmisamp"></a>WmiSamp は、WMI プロバイダーを登録し、フレームワークのプロバイダーのインスタンスにデバイス オブジェクトを作成する方法と、デバイスにアプリケーションを送信する WMI クエリを処理する方法について説明します。

このサンプルの詳細については、次を参照してください。、 [WmiSamp WMI プロバイダー](https://github.com/Microsoft/Windows-driver-samples/tree/master/wmi/wmisamp)します。


