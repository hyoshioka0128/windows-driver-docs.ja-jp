---
title: KMDF ドライバーのサンプル
description: このトピックでは、Windows デベロッパーセンター-ハードウェアからダウンロードできるカーネルモードドライバーフレームワーク (KMDF) サンプルドライバーの一覧を示します。
ms.assetid: 83d15b96-63b1-4584-8ef4-ccbdcc1522bb
keywords:
- カーネルモードドライバー WDK KMDF、サンプル
- KMDF WDK、サンプルドライバー
- カーネルモードドライバーフレームワーク WDK、サンプルドライバー
- フレームワークベースのドライバー WDK KMDF, サンプル
- サンプルドライバー WDK KMDF
ms.date: 06/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: ca1e5c6f45f9158e995175de85a9a27d70264775
ms.sourcegitcommit: 44f09d983954f27fd90b737a2dd142aad7dffd9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70059174"
---
# <a name="sample-kmdf-drivers"></a>KMDF ドライバーのサンプル

このトピックでは、 [Microsoft サンプルポータル](https://docs.microsoft.com/samples/browse/?products=windows-wdk)で参照およびダウンロードできるカーネルモードドライバーフレームワーク (kmdf) サンプルドライバーの一覧を示します。 GitHub で[Windows ドライバーのサンプル](https://github.com/Microsoft/Windows-driver-samples)リポジトリを複製、フォーク、またはダウンロードすることもできます。

サンプルをビルドする方法の詳細については、「[ドライバーのビルド](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)」を参照してください。

<a href="" id="echo"></a>ECHO は、フレームワークのキューおよび要求オブジェクトと自動同期を使用する方法を示しています。

このサンプルの詳細については、 [Kmdf Echo サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/echo/kmdf)を参照してください。

<a href="" id="fakemodem"></a>FakeModem は、コマンドで送受信する単純なモデムなしのモデムドライバーを示しています。

このサンプルの詳細については、「 [Fakemodem ドライバー](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/modem/fakemodem)」を参照してください。

<a href="" id="firefly"></a>FIREFLY、i/o 制御コード (Ioctl) を使用してヒューマン入力デバイス (HID) デバイスをプログラミングする方法を示しています。これは、Windows Management Instrumentation (WMI) インターフェイスを提供します。

このサンプルの詳細については、「 [Firefly filter driver FOR HID device](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/firefly)」を参照してください。

<a href="" id="hidusbfx2"></a>HIDUSBFX2 は、hid デバイスのミニドライバーを作成する方法と、非 HID USB デバイスを HID デバイスにマップする方法を示しています。 デバイスは、OSR USB FX2 Learning Kit に含まれています。

このサンプルの詳細については、「 [HIDUSBFX2](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/hidusbfx2)」を参照してください。

<a href="" id="kbfiltr"></a>KbFiltr は、PS/2 キーボード用の上位デバイスフィルタードライバーを示しています。

このサンプルの詳細については、「[キーボード入力 WDF Filter Driver (Kbfiltr)](https://github.com/Microsoft/Windows-driver-samples/tree/master/input/kbfiltr)」を参照してください。

<a href="" id="ndisprot"></a>NDISProt は、接続がない NDIS 5.0/5.1 および NDIS 6.0 プロトコルドライバーを示しています。

このサンプルの詳細については、「 [NDISPROT WDF Protocol](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/ndis/ndisprot_kmdf)」を参照してください。

<a href="" id="nonpnp"></a>非 PNP は、フレームワークを使用する非プラグアンドプレイ (PnP) ドライバーを示しています。

このサンプルの詳細については、「 [Nonpnp](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/ioctl/kmdf)」を参照してください。

<a href="" id="kmdf-fx2"></a>Kmdf\_FX2 は、OSR usb FX2 Learning Kit に含まれる usb デバイスへのデータ転送を一括して実行する方法を示しています。

このサンプルの詳細については、「 [\_kmdf fx2](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/kmdf_fx2)」を参照してください。

<a href="" id="pcidrv"></a>PCIDRV Intel 82557/82558 ベースの PCI イーサネットアダプター (10/100) と Intel 互換機用の完全に機能するフレームワークベースのドライバー。

このサンプルの詳細については、「 [Pcidrv-WDF Driver FOR PCI Device](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/pcidrv)」を参照してください。

<a href="" id="plx9x5x"></a>PLX9x5x は、DMA をサポートし、PLX9656/9653RDK-LITE ボードを使用する汎用 PCI デバイス用のドライバーを作成する方法を示しています。

このサンプルの詳細については、 [PLX9X5X PCI ドライバー](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/PLX9x5x)を参照してください。

<a href="" id="serial"></a>シリアル: WDM シリアルサンプルドライバーに基づくフレームワークベースのシリアルドライバー。

このサンプルの詳細については、[シリアルサンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serial)を参照してください。

<a href="" id="toaster"></a>トースター Framework ベースのバージョンの WDM トースターサンプルドライバー。 トースターサンプルには、フィルタードライバー、関数ドライバー、および1つのドライバースタックを作成するバスドライバーが含まれています。 このサンプルには、リモート i/o ターゲットを使用してドライバースタックと通信する追加のカーネルモードドライバーも含まれています。

このサンプルの詳細については、「[トースター](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster/toastDrv)」を参照してください。

<a href="" id="usbsamp"></a>UsbSamp は、フレームワークを使用して USB デバイスへの一括およびアイソクロナスデータ転送を実行する方法を示しています。

このサンプルの詳細については、 [Usbsamp サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/usbsamp)を参照してください。

<a href="" id="wmisamp"></a>W誤 Amp では、WMI プロバイダーを登録し、フレームワークのデバイスオブジェクトのプロバイダーインスタンスを作成する方法と、アプリケーションがデバイスに送信する WMI クエリを処理する方法を示します。

このサンプルの詳細については、 [W誤 AMP WMI プロバイダー](https://github.com/Microsoft/Windows-driver-samples/tree/master/wmi/wmisamp)を参照してください。
