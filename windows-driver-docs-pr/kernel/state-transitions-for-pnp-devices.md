---
title: PnP デバイスの状態遷移
description: PnP デバイスの状態遷移
ms.assetid: 31969515-899b-407e-ab73-f6f7f36adb85
keywords:
- PnP WDK カーネル、状態遷移
- WDK カーネルのプラグアンドプレイ状態遷移
- 状態遷移 WDK PnP
- 'デバイスの状態: WDK PnP'
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e8c09d6fc664ea51fd2dacb1bd00b2cba36e425
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838406"
---
# <a name="state-transitions-for-pnp-devices"></a>PnP デバイスの状態遷移


## <a href="" id="ddk-state-transitions-for-pnp-devices-kg"></a>


PnP システムでは、デバイスは、構成されている、開始された、リソースの再調整のために停止された可能性があるため、さまざまな PnP 状態を通じて移行します。 このセクションでは、PnP デバイスの状態の概要について説明します。 概要は、ドライバーで必要とされるほとんどの PnP サポートのためのロードマップです。 このドキュメントの他の部分では、各状態遷移の詳細について説明します。

次の図は、デバイスの PnP 状態と、デバイスがある状態から別の状態に遷移する方法を示しています。

![プラグアンドプレイの観点から見たデバイスの状態を示す図](images/pnp-states.png)

前の図の左上からは、デバイスを挿入したユーザーまたはデバイスが起動時に存在していたため、PnP デバイスが物理的にシステムに存在しています。 デバイスは、システムソフトウェアではまだ認識されていません。

デバイスのソフトウェア構成を開始するには、PnP マネージャーと親バスドライバーがデバイスを列挙します。 PnP マネージャーは、ユーザーモードのコンポーネントからのヘルプを使用して、デバイスのドライバーを識別します。これには、関数ドライバーや任意のフィルタードライバーが含まれます。 PnP マネージャーは、ドライバーがまだ読み込まれていない場合、各ドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンを呼び出します。 PnP デバイスのレポートと列挙の詳細については、「[実行中のシステムへの Pnp デバイスの追加](adding-a-pnp-device-to-a-running-system.md)」を参照してください。

ドライバーが初期化されたら、そのデバイスを初期化する準備ができている必要があります。 PnP マネージャーは、ドライバーが制御する各デバイスに対して、ドライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンを呼び出します。

PnP マネージャーから\_デバイスの要求を開始して、ドライバーが[**IRP\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)を受け取ると、ドライバーはデバイスを起動し、デバイスの i/o 要求を処理する準備が整います。 **\_デバイス要求の開始\_IRP\_** を処理する方法の詳細については、「[デバイスを開始する](starting-a-device.md)」を参照してください。

PnP マネージャーは、アクティブなデバイスのハードウェアリソースを再構成する必要がある場合、 [**irp\_\_クエリを送信し\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)と[**IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)を停止し、デバイスのドライバーへのデバイス要求を停止\_停止します。 ハードウェアリソースを再起動した後、PnP マネージャーは、デバイスを再起動するようにドライバーに指示します。これを行うには、 [**IRP\_完了\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)の要求を開始します。 停止 Irp の処理の詳細については、「[デバイスを停止する](stopping-a-device.md)」を参照してください。 (ブートによって構成されたデバイスのドライバーは、デバイスを起動する前に **\_\_デバイス**と**irp\_** \_を停止する\_クエリを実行することで、irp\_を完了することができます。」を参照してください)。

Windows 98/Me では、PnP マネージャーは、デバイスが無効にされている場合に\_デバイスの要求を停止\_停止する\_デバイスと**irp\_** を**停止する\_\_クエリ**を実行することで、irp\_を送信します。 また、これらのシステム上のドライバーは、障害が発生した開始後にデバイスの要求 **\_\_停止する IRP\_** を受け取ります。

PnP デバイスがシステムから物理的に削除されているか、既に削除されている場合、PnP マネージャーはデバイスのドライバーにさまざまな削除 Irp を送信し、デバイスのソフトウェア表現 (デバイスオブジェクトなど) を削除するように指示します。 削除 Irp の処理の詳細については、「[デバイスの削除](removing-a-device.md)」を参照してください。

ドライバーのすべてのデバイスが削除された後のある時点で、PnP マネージャーはドライバーの[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンを呼び出し、ドライバーをアンロードします。

 

 




