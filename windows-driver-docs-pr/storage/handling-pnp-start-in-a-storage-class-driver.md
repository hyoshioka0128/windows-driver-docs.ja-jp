---
title: 記憶域クラス ドライバーでの PnP 開始の処理
description: 記憶域クラス ドライバーでの PnP 開始の処理
ms.assetid: 8d4ccd09-c5d2-4c9b-b94d-e22c916f0043
keywords:
- 記憶域クラス ドライバー WDK、PnP
- ドライバー WDK の記憶域クラス PnP
- PnP WDK ストレージ
- プラグ アンド プレイ WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbaedafacfcdfe970cee4bf83554126327ee723f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378499"
---
# <a name="handling-pnp-start-in-a-storage-class-driver"></a>記憶域クラス ドライバーでの PnP 開始の処理


## <span id="ddk_handling_pnp_start_in_a_storage_class_driver_kg"></span><span id="DDK_HANDLING_PNP_START_IN_A_STORAGE_CLASS_DRIVER_KG"></span>


ストレージ クラス ドライバー、PnP マネージャーが、クラス ドライバーを呼び出すときに、デバイスに固有の初期化を実行します[ **DispatchPnP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)開始要求をルーチン (IRP\_MJ\_PNP[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device))。 記憶域クラス ドライバーの*DispatchPnP*日常的ないずれかを呼び出す内部*StartDevice*ルーチンまたは同じ機能のインラインを実装します。 FDO に送信された要求を開始する必要があるによって処理されるため最初に、最も低いドライバー スタックでは、記憶域クラス ドライバーの*DispatchPnP*ルーチンで、次の下位ドライバーに要求を転送する[ **保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)呼び出す前に*StartDevice*します。 場合は、要求は、PDO に送信されて、ドライバー必要がありますそれを処理する前に、要求を転送しません。

ストレージ クラス ドライバーの内部*StartDevice*ルーチンは、デバイスの I/O 要求を管理するドライバーにより決定されたデータをその FDO のデバイスの拡張機能を設定します。 詳細については、次を参照してください。[デバイス拡張機能の設定を、記憶域クラス ドライバーの](setting-up-a-storage-class-driver-s-device-extension.md)します。

A *StartDevice*ルーチンは、ドライバーに登録されている任意のデバイスのインターフェイスを有効にする必要があります、 *AddDevice*ルーチン。 (を参照してください[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes))。そのデバイス オブジェクトのシンボリック リンクを作成することも可能性があります。

下のデバイスの開始が完了すると、ドライバーは、ほとんどの場合、デバイスが、D0 電源状態で (上に完全に operational) があると想定できます。 デバイスは完全に電源されませんが、ポート ドライバーは、デバイスが準備できるまでに、要求をキューします。 ただし場合、ドライバーの*StartDevice*ルーチンが突入電流を必要とする操作を実行する必要があります--、たとえば、ディスク ドライブの起動にドライバーする必要があります D0 power に要求を送信、次の下位ドライバー実行する前に、操作です。

ファイルの種類のデバイスのドライバー\_デバイス\_ディスクまたはファイル\_デバイス\_大容量\_ストレージがアイドル状態検出の登録し、標準電源ポリシーのタイムアウトを指定してデバイス クラスの使用-1 の節約とパフォーマンスのタイムアウト値、 **PoRegisterDeviceforIdleDetection**呼び出します。

記憶域クラス ドライバーの詳細については*DispatchPnP*ルーチンを参照してください[記憶域周辺機器への PnP の要求を処理](handling-pnp-requests-to-storage-peripherals.md)します。 PnP 開始要求の処理の詳細については、次を参照してください。[デバイスを起動](https://docs.microsoft.com/windows-hardware/drivers/kernel/starting-a-device)します。

 

 




