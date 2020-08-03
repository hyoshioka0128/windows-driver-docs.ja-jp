---
title: WDM リーダー ドライバー
description: WDM リーダー ドライバー
ms.assetid: ead76f5f-1d28-4343-99c0-e7974fa4c3da
keywords:
- ベンダー提供のドライバー WDK スマートカード、必須ルーチン
- WDM WDK スマートカード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24055cf11fb42aaabb4581ce534032bfd8a85fa4
ms.sourcegitcommit: 20a89aa2cb2c6385c2a49ebf78e5797c821d87ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2020
ms.locfileid: "87473736"
---
# <a name="wdm-reader-driver"></a>WDM リーダー ドライバー

## <a name="required-routines"></a>必須ルーチン

WDM リーダードライバーには、次のルーチンが必要です。

### <a name="driverentry"></a>[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)

ドライバーオブジェクトとディスパッチテーブルを初期化します。

### <a name="adddevice"></a>[AddDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)

スマートカードリーダーのデバイスオブジェクトを作成します。 また、 [AddDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)は、次のいずれかのドライバーライブラリルーチンを呼び出すことができます。

- [Smartcardinitialize (WDM)](https://docs.microsoft.com/previous-versions/ff548944(v=vs.85))を実行してドライバーの初期化を完了します。 [AddDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)でこのルーチンを呼び出すと、加えるになります。
- [Smartcardlogerror (WDM)](https://docs.microsoft.com/previous-versions/ff548947(v=vs.85))によってエラーがログに記録されます。 [Smartcardinitialize (WDM)](https://docs.microsoft.com/previous-versions/ff548944(v=vs.85))が失敗した場合、ドライバーは[AddDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)でこのルーチンを呼び出す必要があります。
- [Smartcardcreatelink (WDM)](https://docs.microsoft.com/previous-versions/ff548935(v=vs.85))を使用して、レジストリにリーダーデバイスのシンボリックリンクを作成します。

### <a name="unload"></a>[取り除き](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)

システムからドライバーを削除します。

### <a name="dispatchcreate"></a>[DispatchCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

および

### <a name="dispatchclose"></a>[DispatchClose](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

では、 [IRP_MJ_CREATE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)と[IRP_MJ_CLOSE&lt](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)をそれぞれサポートしています。 リーダーへの接続を確立するために、リソースマネージャーは**IRP_MJ_CREATE**をリーダードライバーに送信します。 接続を切断するために、リソースマネージャーは**IRP_MJ_CLOSE**を送信します。

### <a name="dispatchcleanup"></a>[DispatchCleanup](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

では[IRP_MJ_CLEANUP](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)がサポートされています。リソースマネージャーはリーダードライバーに送信して、保留中の i/o 要求をキャンセルします。

### <a name="dispatchpnp"></a>[DispatchPnP](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

サポート[IRP_MJ_PNP](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)

### <a name="dispatchpower"></a>[DispatchPower](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[IRP_MJ_POWER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)をサポートします。

### <a name="dispatchdevicecontrol"></a>[DispatchDeviceControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

では[IRP_MJ_DEVICE_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)がサポートされており、スマートカード要求のメインエントリポイントです。 IRP_MJ_DEVICE_CONTROL を受け取ると、 [DispatchDeviceControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)はすぐに[Smartcarddevicecontrol (WDM)](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))を呼び出す必要があります。これは、デバイス制御要求を処理するスマートカードドライバーライブラリルーチンです。 次のコード例は、WDM ドライバーからこのライブラリルーチンを呼び出す方法を示しています。

```cpp
NTSTATUS
DriverDeviceControl(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp
    )
{
    PDEVICE_EXTENSION deviceExtension = DeviceObject -&gt; DeviceExtension;

    return SmartcardDeviceControl(
        &(deviceExtension-&gt;SmartcardExtension),
        Irp
        );
```

呼び出しで示されている特定の IOCTL を処理できない場合、 **Smartcarddevicecontrol**は、不明な ioctl 要求に対してドライバーのコールバックを呼び出します。
