---
title: 記憶域クラス ドライバーでの PnP 開始の処理
description: 記憶域クラス ドライバーでの PnP 開始の処理
ms.assetid: 8d4ccd09-c5d2-4c9b-b94d-e22c916f0043
keywords:
- ストレージクラスドライバー WDK、PnP
- クラスドライバー WDK storage、PnP
- PnP WDK ストレージ
- WDK ストレージのプラグアンドプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c86bab639bba90c3ba0f7cb0d0876d935f14d63
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837555"
---
# <a name="handling-pnp-start-in-a-storage-class-driver"></a>記憶域クラス ドライバーでの PnP 開始の処理


## <span id="ddk_handling_pnp_start_in_a_storage_class_driver_kg"></span><span id="DDK_HANDLING_PNP_START_IN_A_STORAGE_CLASS_DRIVER_KG"></span>


ストレージクラスドライバーは、PnP マネージャーが開始要求を使用してクラスドライバーの[**DispatchPnP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンを呼び出したときに、デバイス固有の初期化を実行します (IRP\_MJ\_Pnp と[**irp\_は\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device))。 ストレージクラスドライバーの*DispatchPnP*ルーチンは、内部*startdevice*ルーチンを呼び出すか、同じ機能をインラインで実装します。 FDO に送信された開始要求は、スタック内の最下位のドライバーによって最初に処理される必要があるため、ストレージクラスドライバーの*DispatchPnP*ルーチンは、 *startdevice*を呼び出す前に[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を使用して、次の下位のドライバーに要求を転送します。 要求が PDO に送信された場合、ドライバーは、要求を処理する前に転送する必要がありません。

ストレージクラスドライバーの内部*Startdevice*ルーチンは、デバイスの i/o 要求を管理するために、ドライバーによって決定されたデータを使用して、その FDO のデバイス拡張機能を設定します。 詳細については、「[ストレージクラスドライバーのデバイス拡張機能](setting-up-a-storage-class-driver-s-device-extension.md)のセットアップ」を参照してください。

*Startdevice*ルーチンは、ドライバーによって*AddDevice*ルーチンに登録されたデバイスインターフェイスを有効にする必要があります。 (「[デバイスインターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)」を参照してください)。また、デバイスオブジェクトのシンボリックリンクを作成する場合もあります。

低いデバイスの開始が完了した後、ドライバーはデバイスが D0 (完全に動作) されていると想定できます。 デバイスの電源が完全に切れていない場合、ポートドライバーはデバイスの準備が整うまで要求をキューに入れます。 ただし、ドライバーの*Startdevice*ルーチンで、突入電流を必要とする操作 (ディスクドライブのスピンアップなど) を実行する必要がある場合は、操作を実行する前に、ドライバーが次の下位のドライバーに D0 の電源要求を送信する必要があります。

デバイスの種類がファイル\_デバイスのドライバー\_ディスクまたはファイル\_デバイス\_大容量\_ストレージでは、アイドル検出に登録して、節約とパフォーマンスを指定することにより、デバイスクラスの標準の電源ポリシーのタイムアウトを使用することができます。**PoRegisterDeviceforIdleDetection**呼び出しのタイムアウト値-1。

ストレージクラスドライバーの*DispatchPnP*ルーチンの詳細については、「[ストレージ周辺機器への PnP 要求の処理](handling-pnp-requests-to-storage-peripherals.md)」を参照してください。 PnP 開始要求の処理の詳細については、「[デバイスを開始する](https://docs.microsoft.com/windows-hardware/drivers/kernel/starting-a-device)」を参照してください。

 

 




