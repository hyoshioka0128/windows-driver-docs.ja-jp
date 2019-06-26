---
title: ドライバーの I/O スタック位置を確認すべき場合
description: ドライバーの I/O スタック位置を確認すべき場合
ms.assetid: ca084221-7b07-4db0-a987-9dd8a66d169c
keywords:
- ディスパッチ ルーチンの WDK カーネル、I/O スタックの場所
- I/O スタックの場所 WDK ディスパッチ ルーチン
- スタックの場所の I/O ドライバー WDK ディスパッチ ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8325c640c005bc66a6b5e828f07cf20d193f94f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358112"
---
# <a name="when-to-check-the-drivers-io-stack-location"></a>ドライバーの I/O スタック位置を確認すべき場合





ドライバーの主要な I/O 関数のコードが設定されて[I/O スタックの場所](i-o-stack-locations.md)各着信 IRP の。

ドライバーのディスパッチ ルーチンは、ドライバーの場合は、次の条件のいずれかの対処方法を決定する IRP の I/O スタックの場所を確認する必要があります。

-   ディスパッチ ルーチンは、1 つ以上の主要な I/O 関数コードを処理します。

-   ディスパッチ ルーチンは、一連の特定の主な機能コードの軽微な関数のコードを処理する必要があります。 コードを含めるマイナー関数を使用した Irp [ **IRP\_MJ\_PNP** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)と[ **IRP\_MJ\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)に加えて、特定の Irp SCSI ポート ドライバーとファイル システム ドライバーを処理する必要があります。

-   ディスパッチ ルーチンまたは密接に結合されたより高度なドライバーのデバイス ドライバーの処理[ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)または[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)要求で、関連付けられている I/O 制御コードのセットがあります。

ルーチンの呼び出しのドライバーの I/O スタックの場所、そのディスパッチへのポインターを取得する[ **IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)します。

常に上位レベルのドライバーのディスパッチ ルーチンを呼び出して**IoGetCurrentIrpStackLocation**を呼び出すことも、 [ **IoGetNextIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetnextirpstacklocation)次の下位にポインターを取得するには次の下位ドライバーのセットアップが Irp のドライバーの I/O スタックの場所と[ドライバー スタックを Irp を渡して](passing-irps-down-the-driver-stack.md)します。

[ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンまたは[ *DispatchInternalDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)のデバイス ドライバー、または場合によってはの日常的な密接に結合されたクラスのドライバーが I/O 制御コードは、ドライバーの I/O スタック位置で設定を決定する必要があります**Parameters.DeviceIoControl.IoControlCode**要求ごとにします。 I/O 制御コードは、ドライバーの I/O スタックの場所に格納されます。

ほとんどの場合、 *DispatchDeviceControl*または*DispatchInternalDeviceControl*より高度なドライバーのルーチンに渡すだけです、 **IRP\_MJ\_デバイス\_コントロール**または**IRP\_MJ\_内部\_デバイス\_コントロール**要求をそのスタックを設定した後、次の下位ドライバーIRP 内の位置。 ただし、SCSI クラス ドライバーを特定の確認する必要があります[SCSI ポート I/O 制御コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)が設定できるように、SCSI ポート ドライバーの I/O スタックの場所を正しくこれらの要求を渡す前にします。

 

 




