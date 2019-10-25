---
title: WDF HID ミニドライバーの作成
description: このトピックでは、Windows Driver Framework (WDF) を使用してヒューマンインターフェイスデバイス (HID) ミニドライバーを作成する方法について説明します。
ms.assetid: 4FEDFE4B-F3B2-4B34-80DC-84BFFA4C612B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 833cd492992c9679a0812d1a5394c3060e7be1cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844675"
---
# <a name="creating-wdf-hid-minidrivers"></a>WDF HID ミニドライバーの作成


このトピックでは、Windows Driver Framework (WDF) を使用してヒューマンインターフェイスデバイス (HID) ミニドライバーを作成する方法について説明します。

KMDF または UMDF を使用して HID ミニドライバーを作成できます。 Vhidmini2 ミニドライバーサンプルから始めることをお勧めします。 このサンプルドライバーは、KMDF または UMDF 2.x を使用してコンパイルできます。

**提供するもの**

1.  下のフィルタードライバーは、 *MsHidUmdf* (UMDF の場合) または*MsHidKmdf* (kmdf の場合) の下に記述します。これらはいずれもオペレーティングシステムの一部として含まれています。
2.  [Vhidmini2 サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/vhidmini2)をダウンロードして確認します。

3.  ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数から[**WdfFdoInitSetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetfilter)を呼び出します。

4.  I/o キューを作成して、 *MsHidUmdf*または*MsHidKmdf*がクラスドライバーからドライバーに渡す i/o 要求を受信します。

5.  IOCTL 固有のメソッドハンドラーに分岐する[*Evtiodevicecontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)コールバック関数を指定します。 [WDF HID ミニドライバー ioctl](https://docs.microsoft.com/previous-versions/hh463977(v=vs.85))で説明されている ioctl を確認し、デバイスに関連するものがドライバーで処理されることを確認します。
6.  UMDF の場合、ドライバーが ACPI によって列挙されている場合は、必要に応じてセレクティブサスペンドを有効にします。 デバイスのハードウェアキーで、 **EnableDefaultIdleNotificationHandler**サブキーを追加し、それを1に設定します。
7.  UMDF の場合は、INF ファイルの WDF 固有の*Ddinstall*セクションで次の[inf ディレクティブ](specifying-wdf-directives-in-inf-files.md)を設定します。

    -   カーネルモードのパススルードライバーをスタックに読み込むことができるように、 **Allowdfkernel Modeclientpolicy を allowdfに**設定します。
    -   **Umdfmethodneino action**を**コピー**して、UMDF がメソッドの ioctl を処理できるように\_します。
    -   **Umdffileobjectpolicy**を**AllowNullAndUnknownFileObjects**に
    -   **UmdfFsContextUsePolicy** **CanUseFsContext2**

    次に、例を示します。

    ```cpp
    [hidumdf.NT.Wdf]
    UmdfKernelModeClientPolicy = AllowKernelModeClients
    UmdfMethodNeitherAction=Copy
    UmdfFileObjectPolicy=AllowNullAndUnknownFileObjects
    UmdfFsContextUsePolicy = CanUseFsContext2
    ```

Windows 7 用の UMDF HID ミニドライバーを作成している場合は、 [Windows Driver Kit (WDK) 8.1](https://go.microsoft.com/fwlink/p/?LinkId=733614)をダウンロードして、 *hidumdf*のソースコードを取得します。 次に、UMDF 1.11 ドライバーを記述し、ドライバーパッケージに*hidumdf .sys*と umdf 1.11 を含めます。

## <a name="architecture"></a>Architecture


HID クラスドライバー (*HidClass*) とフレームワークは、競合する WDM ディスパッチルーチンを提供して、ミニドライバーの一部の i/o 要求 (プラグアンドプレイや電源管理要求など) を処理します。 その結果、HID ミニドライバーはクラスドライバーとフレームワークの両方にリンクできません。 そのため、Microsoft は*MsHidUmdf*と*MsHidKmdf*を提供しています。これは、クラスドライバーとミニドライバーの間に存在する WDM ドライバーです。

*MsHidUmdf*と*MsHidKmdf*はどちらも、実際の hid ミニドライバーとして登録するために、Hid クラスドライバーの[**HidRegisterMinidriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidport/nf-hidport-hidregisterminidriver)ルーチンを呼び出します。 これらのドライバーはデバイスの関数ドライバーとして機能しますが、クラスドライバーからドライバーに i/o 要求を渡すだけです (これは*パススルードライバー*と呼ばれることもあります)。 KMDF と UMDF の両方で、指定するコンポーネントは HID ミニドライバーだけです。これは、パススルードライバーの下にあるフィルタードライバーの下位にあります。

|                                                                                     |                                                                                        |
|-------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| UMDF アーキテクチャ                                                                   | KMDF アーキテクチャ                                                                      |
| ![ドライバースタック内の hidumdf .sys の場所](images/UMDF-basedHIDMinidrivers.png) | ![ドライバースタック内の mshidkmdf の場所](images/Framework-basedHIDMinidrivers.png) |

 

 

 





