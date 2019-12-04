---
title: USB (ユニバーサル シリアル バス) ドライバーのサンプル
description: このディレクトリのドライバーサンプルは、デバイスのカスタム USB ドライバーを作成するための開始点となります。
ms.assetid: 4A61F62B-9C23-4265-8AB4-D3AB45F512DF
ms.date: 12/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6439e1dc217ed9b51972e4c55bee81caf64af660
ms.sourcegitcommit: 30fa63ad13fd5e2e883b76a44f0703e01049ffa1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74735166"
---
# <a name="universal-serial-bus-usb-driver-samples"></a>USB (ユニバーサル シリアル バス) ドライバーのサンプル

このディレクトリのドライバーサンプルは、デバイスのカスタム USB ドライバーを作成するための開始点となります。

| サンプル | 説明 |
| --- | --- |
| [KMDF バスドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/sample-kmdf-bus-driver-for-osr-usb-fx2) | FX2 デバイスで、バスドライバーに KMDF を使用する方法を示します。 |
| [OSR USB-FX2 用の KMDF 関数ドライバーのサンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/sample-kmdf-function-driver-for-osr-usb-fx2) | USB デバイスへのデータ転送の一括および中断を実行する方法を示します。 このサンプルは、OSR USB FX2 Learning Kit 用に書かれています。 |
| [USB 関数クライアントドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/usb-function-client-driver) | USB 関数クラス拡張ドライバー (UFX) を使用して Windows USB 関数コントローラードライバーを作成する方法を示すスケルトンサンプルドライバー。 |
| [FX2 の KMDF 関数ドライバーの上にある UMDF フィルターのサンプル (UMDF 1)](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/sample-umdf-filter-above-kmdf-function-driver-for-osr-usb-fx2-umdf-version-1) | UMDF フィルタードライバーを kmdf\_fx2 サンプルドライバーの上位フィルタードライバーとして読み込む方法を示します。 このサンプルは、OSR USB FX2 Learning Kit 用に書かれています。 |
| [OSR FX2 の UMDF 関数ドライバーの上にある UMDF フィルターのサンプル (UMDF 1)](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/sample-umdf-filter-above-umdf-function-driver-for-osr-usb-fx2-umdf-version-1) | umdf\_fx2 サンプルドライバーの上位フィルタードライバーとして、UMDF フィルタードライバーを読み込む方法を示します。 このサンプルは、OSR USB FX2 Learning Kit 用に書かれています。 |
| [UMDF 1 関数ドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/sample-umdf-function-driver-for-osr-usb-fx2-umdf-version-1) | OSR USB FX2 デバイス用のユーザーモードドライバーフレームワーク (UMDF 1) ドライバー。 これには、テストアプリケーションとサンプルデバイスのメタデータが含まれ、偽装とアイドル状態の電源がサポートされます。 |
| [UMDF 2 関数ドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/sample-function-driver-for-osr-usb-fx2-umdf-version-2) | OSR USB FX2 デバイス用のユーザーモードドライバーフレームワーク (UMDF 2) ドライバー。 これには、テストアプリケーションとサンプルデバイスのメタデータが含まれ、偽装とアイドル状態の電源がサポートされます。 |
| [USBSAMP 汎用 USB ドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/usbsamp-generic-usb-driver) | 汎用 USB デバイスの一括およびアイソクロナスエンドポイントとの間で高速で高速な転送を実行する方法を示します。 |
| [USBView](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/usbview-sample-application) | システム上のすべての USB コントローラーと接続されている USB デバイスを参照できる Windows アプリケーション。 |
| [WDF FX2 のサンプルドライバーの学習ラボ](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/wdf-sample-driver-learning-lab-for-osr-usb-fx2) | コンソールテストアプリケーションと、KMDF と UMDF バージョン1の両方に対応する一連の反復ドライバーが含まれています。 |
| [UcmCxUcsi ポートコントローラークライアントドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/ucmtcpcicx-port-controller-client-driver-v2) | USB コネクタマネージャークラス拡張ドライバー (UcmCx) を使用して、Windows USB タイプ C ポートコントローラードライバーを作成する方法を示します。 |
| [UcmTcpciCx ポートコントローラークライアントドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/ucmtcpcicx-port-controller-client-driver) | USB コネクタマネージャータイプ C ポートコントローラーインターフェイスクラス拡張ドライバー (UcmTcpciCx) を使用して、Windows USB タイプ C ポートコントローラードライバーを作成する方法を示します。
| [UcmUcsiCx ACPI クライアントドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/ucmucsicx-acpi-client-driver) | USB コネクタマネージャークラス拡張ドライバー (UcmCx) を使用して、UCSI 準拠 (ACPI トランスポート) Windows USB タイプ C ポートコントローラードライバーを作成する方法を示します。 |
