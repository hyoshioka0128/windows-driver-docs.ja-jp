---
title: WDF HID ミニドライバーの作成
description: このトピックでは、Windows Driver Framework (WDF) を使用してヒューマンインターフェイスデバイス (HID) ミニドライバーを作成する方法について説明します。
ms.assetid: 4FEDFE4B-F3B2-4B34-80DC-84BFFA4C612B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6347ab0e1367a2c348d73db196c90704fb1e0e2
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968533"
---
# <a name="creating-wdf-hid-minidrivers"></a>WDF HID ミニドライバーの作成


このトピックでは、Windows Driver Framework (WDF) を使用してヒューマンインターフェイスデバイス (HID) ミニドライバーを作成する方法について説明します。

KMDF または UMDF を使用して HID ミニドライバーを作成できます。 Vhidmini2 ミニドライバーサンプルから始めることをお勧めします。 このサンプルドライバーは、KMDF または UMDF 2.x を使用してコンパイルできます。

**提供するもの**

1.  *MsHidUmdf.sys* (UMDF の場合) または*MsHidKmdf.sys* (kmdf の場合) の下に低いフィルタードライバーを記述します。これらはいずれもオペレーティングシステムの一部として含まれています。
2.  [Vhidmini2 サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/vhidmini2)をダウンロードして確認します。

3.  ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数から[**WdfFdoInitSetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetfilter)を呼び出します。

4.  I/o キューを作成し、 *MsHidUmdf.sys*またはクラスドライバーからドライバーへの*MsHidKmdf.sys*渡す i/o 要求を受信します。

5.  IOCTL 固有のメソッドハンドラーに分岐する[*Evtiodevicecontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)コールバック関数を指定します。 [WDF HID ミニドライバー ioctl](https://docs.microsoft.com/previous-versions/hh463977(v=vs.85))で説明されている ioctl を確認し、デバイスに関連するものがドライバーで処理されることを確認します。
6.  UMDF の場合、ドライバーが ACPI によって列挙されている場合は、必要に応じてセレクティブサスペンドを有効にします。 デバイスのハードウェアキーで、 **EnableDefaultIdleNotificationHandler**サブキーを追加し、それを1に設定します。
7.  UMDF の場合は、INF ファイルの WDF 固有の*Ddinstall*セクションで次の[inf ディレクティブ](specifying-wdf-directives-in-inf-files.md)を設定します。

    -   カーネルモードのパススルードライバーをスタックに読み込むことができるように、 **Allowdfkernel Modeclientpolicy を allowdfに**設定します。 **AllowKernelModeClients**
    -   **Umdfmethodneino action**を**コピー**することにより、UMDF は、メソッドのいずれの型にも ioctl を処理できませ \_ ん。
    -   **Umdffileobjectpolicy**を**AllowNullAndUnknownFileObjects**に
    -   **UmdfFsContextUsePolicy** **CanUseFsContext2**

    次に例を示します。

    ```cpp
    [hidumdf.NT.Wdf]
    UmdfKernelModeClientPolicy = AllowKernelModeClients
    UmdfMethodNeitherAction=Copy
    UmdfFileObjectPolicy=AllowNullAndUnknownFileObjects
    UmdfFsContextUsePolicy = CanUseFsContext2
    ```

Windows 7 用の UMDF HID ミニドライバーを作成している場合は、 [Windows Driver Kit (WDK) 8.1](https://go.microsoft.com/fwlink/p/?LinkId=733614)をダウンロードして*HidUmdf.sys*のソースコードを取得します。 次に、UMDF 1.11 ドライバーを記述し、ドライバーパッケージに*HidUmdf.sys*と umdf 1.11 を含めます。

## <a name="architecture"></a>アーキテクチャ


HID クラスドライバー (*HidClass.sys*) とフレームワークは、競合する WDM ディスパッチルーチンを提供して、ミニドライバーに対する一部の i/o 要求 (プラグアンドプレイや電源管理要求など) を処理します。 その結果、HID ミニドライバーはクラスドライバーとフレームワークの両方にリンクできません。 そのため、Microsoft は*MsHidUmdf.sys*と*MsHidKmdf.sys*を提供しています。これは、クラスドライバーとミニドライバーの間に存在する WDM ドライバーです。

*MsHidUmdf.sys*と*MsHidKmdf.sys*はどちらも、実際の hid ミニドライバーとして登録するために、Hid クラスドライバーの[**HidRegisterMinidriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidport/nf-hidport-hidregisterminidriver)ルーチンを呼び出します。 これらのドライバーはデバイスの関数ドライバーとして機能しますが、クラスドライバーからドライバーに i/o 要求を渡すだけです (これは*パススルードライバー*と呼ばれることもあります)。 KMDF と UMDF の両方で、指定するコンポーネントは HID ミニドライバーだけです。これは、パススルードライバーの下にあるフィルタードライバーの下位にあります。

**UMDF アーキテクチャ**: kmdf アーキテクチャ

** ![ ドライバースタック内の hidumdf.sys の場所](images/UMDF-basedHIDMinidrivers.png)**: ![ ドライバースタック内の mshidkmdf.sys の場所](images/Framework-basedHIDMinidrivers.png)


 

 

 





