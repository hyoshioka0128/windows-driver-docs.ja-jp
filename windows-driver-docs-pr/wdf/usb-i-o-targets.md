---
title: USB I/O ターゲット
description: このセクションでは、KMDF および UMDF 2 ドライバーがユニバーサルシリアルバス (USB) デバイスと対話する方法について説明します。
ms.assetid: 195c0f4b-7f33-428a-8de7-32643ad854c6
keywords:
- I/o ターゲット (WDK KMDF、USB)
- USB i/o ターゲット (WDK KMDF)
- USB 要求が WDK KMDF をブロックする
- URBs WDK KMDF
- USB i/o ターゲット WDK KMDF、USB i/o ターゲットについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 163ba4f1a1766b378dc86397322df0b7c7a62ab2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843111"
---
# <a name="usb-io-targets"></a>USB I/O ターゲット


このセクションでは、バージョン2以降のカーネルモードドライバーフレームワーク (KMDF) ドライバーとユーザーモードドライバーフレームワーク (UMDF) ドライバーが universal serial bus (USB) デバイスを操作する方法について説明します。




各 USB デバイスと、USB デバイスインターフェイスがサポートする各パイプには、個別の i/o ターゲットがあります。 USB デバイスが処理する制御転送は、デバイスの i/o ターゲットに送信されます。 特定のパイプハンドルを対象とする i/o 転送は、そのパイプの i/o ターゲットに送信されます。

フレームワークは、usb 要求ブロック ([**URBs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)) を送信することによって、usb デバイスの i/o ターゲットと通信します。 フレームワークには、ドライバーから URBs を非表示にするオブジェクトメソッドが用意されています。これにより、ドライバー自体をビルドして送信する必要がなくなります。 ドライバーのビルドを URBs する場合、KMDF ドライバーは、URBs をビルドして送信するオブジェクトメソッドの追加のセットを使用できます。

USB デバイスに必要なドライバーの種類を決定する方法の詳細については、「 [usb クライアントドライバーを開発するためのドライバーモデルの選択](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

このセクションの内容:

-   [USB デバイスの操作](working-with-usb-devices.md)

-   [USB インターフェイスの使用](working-with-usb-interfaces.md)

-   [USB パイプの使用](working-with-usb-pipes.md)

 

 





