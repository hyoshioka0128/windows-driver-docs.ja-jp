---
title: WDM デバイス スタックの例
description: WDM デバイス スタックの例
ms.assetid: 1128e098-9ef4-4bc3-aa09-74df3142fb11
keywords:
- デバイススタック WDK カーネル、例
- ジョイスティックの WDK デバイススタック
- 機能デバイスオブジェクト WDK カーネル
- FDO WDK カーネル
- 物理デバイスオブジェクト WDK カーネル
- PDOs WDK カーネル
- DOs WDK カーネルをフィルター処理する
- USB ハブデバイススタックの WDK カーネル
- USB ホストコントローラーデバイススタックの WDK カーネル
- PCI バスデバイススタック WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e125f85bf82705e8c961d625d447c10ddf608b0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836729"
---
# <a name="example-wdm-device-stack"></a>WDM デバイス スタックの例





ここでは、WDM デバイスオブジェクトとその階層化の方法を示すために、USB ハードウェア用の一連のドライバーによって作成されるデバイスオブジェクトについて説明します。

次の図は、「 [WDM ドライバーレイヤー: 例](wdm-driver-layers---an-example.md)」で説明されているサンプルドライバーによって作成されたデバイスオブジェクトを示しています。

![usb ジョイスティックのサンプルの wdm デバイスオブジェクトレイヤーを示す図](images/joydobj.png)

この図の下部から、デバイスのサンプルスタックには次のオブジェクトが含まれています。

1.  PCI バスの PDO と FDO。

    ルートバスドライバーは、内部システムバス (ルートバス) を列挙し、検出された各デバイスの PDO を作成します。 これらの PDOs の1つは PCI バス用です。 (ルートバスの PDO と FDO は、図には示されていません)。

    PnP マネージャは pci ドライバを PCI バスのファンクションドライバとして識別し、ドライバを読み込んで (まだ読み込まれていない場合)、PDO を PCI ドライバに渡します。 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンでは、pci ドライバーは pci バス ([**IOCREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)) の FDO を作成し、pci バスのデバイススタック ([**Ioattachdevicetodevicestack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)) に FDO を関連付けます。 Pci ドライバーは、PCI バスの関数ドライバーとして、この FDO を作成し、その役割の一部としてアタッチします。

    この例では、PCI バス用のフィルタードライバーはありません。

2.  USB ホストコントローラーの PDO と FDO。

    PnP マネージャは、PCI ドライバにデバイスを起動するように指示します (Irp\_によって[ **\_デバイスが起動さ\_開始**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)されます)。次に、その子に対して pci ドライバにクエリを実行します ([**irp\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations) 、\_デバイス\_の関係**Busrelations**の関係の種類。 応答として、PCI ドライバーはバス上のデバイスを列挙します。 この例では、PCI ドライバーが USB ホストコントローラーを検出し、そのデバイス用の PDO を作成します。 図の幅の広い矢印は、USB ホストコントローラーが PCI バスの "子" であることを示しています。 PCI ドライバーは、PCI バスのバスドライバーとしての役割の一部として、その子デバイスの PDOs を作成します。

    PnP マネージャーは、usb ホストコントローラーの miniclass/クラスドライバーペアを USB ホストコントローラーの関数ドライバーとして識別し、ドライバーのペアを読み込みます。 PnP マネージャーは、適切なタイミングでドライバーペアを呼び出して、USB ホストコントローラーの FDO を作成して接続します。

    この例では、USB ホストコントローラー用のフィルタードライバーはありません。

3.  USB ハブの PDO と FDO。

    USB ホストコントローラーは、そのバスを列挙し、唯一のポートで USB ハブを特定し、ハブ用の PDO を作成します。 USB ハブドライバーは、ハブの FDO を作成して接続します。

    この例では、USB ハブ用のフィルタードライバーはありません。

4.  ジョイスティックデバイス用の PDO、FDO、および2つのフィルター DOs。

    USB ハブドライバーは、バスを列挙し、HID デバイス (ジョイスティック) を特定して、ジョイスティック用の PDO を作成します。

    この例では、ジョイスティックデバイスの下位レベルのフィルタードライバーがレジストリに設定されているため、PnP マネージャーはフィルタードライバーを読み込みます。 フィルタードライバーは、デバイスに関連するものと判断し、デバイススタックに対してフィルター処理を作成してアタッチします。

    PnP マネージャーは、ジョイスティックデバイスの関数ドライバーが HID class/miniclass ドライバーのペアであることを判断し、それらのドライバーを読み込みます。 ドライバーのペアは、クラスドライバーの DLL にリンクされている miniclass ドライバーで構成されます。同時に、デバイスの1つの関数ドライバーとして機能します。 クラス/miniclass ドライバーのペアは、1つのデバイスオブジェクトと FDO を作成し、デバイススタックにアタッチします。

    上位レベルのフィルタードライバーは、下位レベルのフィルターと同様の方法で、フィルターを作成してデバイススタックにアタッチします。

親バスドライバーによって作成される PDO は、常に特定のデバイスのデバイススタックの一番下にあることに注意してください。 ドライバーが PnP または電源 Irp を処理するときは、各 IRP を、デバイススタックから PDO および関連付けられているバスドライバーに渡す必要があります。

次の図は、前の図と同じデバイススタックを示していますが、どのデバイスオブジェクトがどのドライバーによって作成および管理されているかを強調しています。

![ドライバーの観点から見たサンプルデバイスオブジェクトレイヤーを示す図](images/joydobj2.png)

バスドライバーが複数のデバイススタックにまたがっています。 バスドライバーは、バスアダプター/コントローラーの FDO を作成し、その子デバイスごとに PDO を作成します。

 

 




