---
title: WDM デバイス スタックの例
description: WDM デバイス スタックの例
ms.assetid: 1128e098-9ef4-4bc3-aa09-74df3142fb11
keywords:
- デバイス履歴の WDK カーネル、例
- ジョイスティック WDK デバイス スタック
- 機能のデバイス オブジェクトの WDK カーネル
- FDO WDK カーネル
- 物理デバイス オブジェクトの WDK カーネル
- Pdo WDK カーネル
- フィルター DOs WDK カーネル
- USB ハブ デバイス スタック WDK カーネル
- USB ホスト コント ローラー デバイス スタック WDK カーネル
- PCI バス デバイス スタック WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65a6322774673e9dea5a34c892054b96a25d0ab2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386629"
---
# <a name="example-wdm-device-stack"></a>WDM デバイス スタックの例





このセクションでは、可能な一連の WDM デバイス オブジェクトと階層化する方法を説明するために USB ハードウェアのドライバーによって作成されたデバイス オブジェクトについて説明します。

次の図で説明されているサンプル ドライバーによって作成されたデバイス オブジェクト[WDM ドライバー レイヤー。たとえば](wdm-driver-layers---an-example.md)します。

![usb ジョイスティックのサンプル wdm デバイス オブジェクト レイヤーを示す図](images/joydobj.png)

この図の下部にある以降は、サンプル デバイス スタックでデバイス オブジェクトが含まれます。

1.  PDO の PCI バス FDO.

    ルートのバス ドライバーでは、内部システム バス (ルート バス) を列挙し、見つかった各デバイスの PDO を作成します。 これらの Pdo の 1 つは、PCI バスです。 (PDO とルート bus FDO は表示されません図。)

    PnP マネージャーは、PCI バスの機能のドライバーには (これはまだ読み込まれていない) 場合、ドライバーが読み込まれる PCI ドライバを識別し、PCI ドライバーの PDO を渡します。 その[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチン、PCI バス FDO は PCI ドライバに作成します ([**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)) し、デバイスに、FDO をアタッチします。スタック ([**IoAttachDeviceToDeviceStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)) PCI バス。 PCI ドライバは、作成し、PCI バスの機能のドライバーとしての役割の一部としてこの FDO をアタッチします。

    この例では、PCI バスのフィルター ドライバーはありません。

2.  PDO の USB ホスト コント ローラー FDO.

    PnP マネージャーがそのデバイスを開始する PCI ドライバを指示 ([**IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)) とその子の PCI ドライバをクエリ ([ **IRP\_MN\_クエリ\_デバイス\_リレーション**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)の関係の種類と**BusRelations**)。 応答では、PCI ドライバは、そのバス上のデバイスを列挙します。 この例では、PCI ドライバは、USB ホスト コント ローラーを検索し、そのデバイス用の PDO を作成します。 幅の広い矢印の図には、USB ホスト コント ローラーが PCI バスの「子」であることを示します。 PCI ドライバは、PCI バスのバス ドライバー コンポーネントの役割の一部としてデバイス、その子の Pdo を作成します。

    PnP マネージャーでは、関数のドライバーを USB ホスト コント ローラーとして、USB ホスト コント ローラー miniclass/クラス ドライバーのペアを識別し、ドライバーのペアを読み込みます。 PnP マネージャーでは、作成して FDO の USB ホスト コント ローラーを接続する適切なタイミングでドライバーのペアを呼び出します。

    この例では、USB ホスト コント ローラーのフィルター ドライバーはありません。

3.  PDO の USB ハブ FDO.

    USB ホスト コント ローラーは、バスを列挙、唯一のポートに USB ハブを検索し、ハブの PDO を作成します。 USB ハブのドライバーでは、作成し、ハブの FDO をアタッチします。

    この例では、USB ハブ用のフィルター ドライバーはありません。

4.  PDO、FDO、および 2 つは、DOs ジョイスティック デバイスのフィルター処理します。

    USB ハブのドライバーは、そのバスを列挙、HID デバイス (ジョイスティック) を検索し、ジョイスティックの PDO を作成します。

    この例では、下位レベルのフィルター ドライバーが設定されてジョイスティックのデバイス用にレジストリで、PnP マネージャーが、フィルター ドライバーを読み込むように。 フィルター ドライバーと判断がデバイスに関連して作成し、デバイス スタックにはフィルターをアタッチします。

    PnP マネージャーでは、ジョイスティックのデバイスの機能のドライバーは HID クラス/miniclass ドライバーのペアは、し、それらのドライバーを読み込みますを決定します。 ドライバーのペアから成るクラス ドライバー DLL にリンクされている miniclass ドライバーまとめて、デバイスの 1 つの関数ドライバーとして機能します。 クラス/miniclass ドライバーのペアは、FDO、1 つのデバイス オブジェクトを作成し、デバイス スタックに結び付けます。

    上位レベルのフィルター ドライバーは、作成し、下位レベルのフィルターと同様の方法で、デバイス スタックにフィルター操作を結び付けます。

親のバス ドライバーによって作成された PDO は常に特定のデバイスのデバイス スタックの下部にあることに注意してください。 ドライバーの PnP 処理ときに、または電源 Irp、デバイス スタックの一番下には、各 IRP PDO とその関連付けられているバス ドライバーに渡す必要があります。

次の図は、前の図と同じデバイス スタックを示していますが、デバイス オブジェクトが作成され、どのドライバーによって管理される強調されています。

![ドライバーの観点からのサンプル デバイス オブジェクト レイヤーを示す図](images/joydobj2.png)

バス ドライバーでは、1 つ以上のデバイス スタックにまたがります。 バス ドライバーでは、そのバス アダプタ/コント ローラーの FDO を作成し、デバイスごとの子の PDO を作成します。

 

 




