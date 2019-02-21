---
title: ドライバーの I/O スタックの場所を確認します。
description: ドライバーの I/O スタックの場所を確認します。
ms.assetid: ca084221-7b07-4db0-a987-9dd8a66d169c
keywords:
- ディスパッチ ルーチンの WDK カーネル、I/O スタックの場所
- I/O スタックの場所 WDK ディスパッチ ルーチン
- スタックの場所の I/O ドライバー WDK ディスパッチ ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 527f3bc56d1b775828426bc59a4e0764cfc0d5c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537726"
---
# <a name="when-to-check-the-drivers-io-stack-location"></a>ドライバーの I/O スタックの場所を確認します。





ドライバーの主要な I/O 関数のコードが設定されて[I/O スタックの場所](i-o-stack-locations.md)各着信 IRP の。

ドライバーのディスパッチ ルーチンは、ドライバーの場合は、次の条件のいずれかの対処方法を決定する IRP の I/O スタックの場所を確認する必要があります。

-   ディスパッチ ルーチンは、1 つ以上の主要な I/O 関数コードを処理します。

-   ディスパッチ ルーチンは、一連の特定の主な機能コードの軽微な関数のコードを処理する必要があります。 コードを含めるマイナー関数を使用した Irp [ **IRP\_MJ\_PNP** ](https://msdn.microsoft.com/library/windows/hardware/ff550772)と[ **IRP\_MJ\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff550784)に加えて、特定の Irp SCSI ポート ドライバーとファイル システム ドライバーを処理する必要があります。

-   ディスパッチ ルーチンまたは密接に結合されたより高度なドライバーのデバイス ドライバーの処理[ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)または[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)要求で、関連付けられている I/O 制御コードのセットがあります。

ルーチンの呼び出しのドライバーの I/O スタックの場所、そのディスパッチへのポインターを取得する[ **IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)します。

常に上位レベルのドライバーのディスパッチ ルーチンを呼び出して**IoGetCurrentIrpStackLocation**を呼び出すことも、 [ **IoGetNextIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549266)次の下位にポインターを取得するには次の下位ドライバーのセットアップが Irp のドライバーの I/O スタックの場所と[ドライバー スタックを Irp を渡して](passing-irps-down-the-driver-stack.md)します。

[ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンまたは[ *DispatchInternalDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)のデバイス ドライバー、または場合によってはの日常的な密接に結合されたクラスのドライバーが I/O 制御コードは、ドライバーの I/O スタック位置で設定を決定する必要があります**Parameters.DeviceIoControl.IoControlCode**要求ごとにします。 I/O 制御コードは、ドライバーの I/O スタックの場所に格納されます。

ほとんどの場合、 *DispatchDeviceControl*または*DispatchInternalDeviceControl*より高度なドライバーのルーチンに渡すだけです、 **IRP\_MJ\_デバイス\_コントロール**または**IRP\_MJ\_内部\_デバイス\_コントロール**要求をそのスタックを設定した後、次の下位ドライバーIRP 内の位置。 ただし、SCSI クラス ドライバーを特定の確認する必要があります[SCSI ポート I/O 制御コード](https://msdn.microsoft.com/library/windows/hardware/ff565367)が設定できるように、SCSI ポート ドライバーの I/O スタックの場所を正しくこれらの要求を渡す前にします。

 

 




