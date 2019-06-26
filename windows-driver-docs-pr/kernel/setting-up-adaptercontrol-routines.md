---
title: AdapterControl ルーチンのセットアップ
description: AdapterControl ルーチンのセットアップ
ms.assetid: 0d2add25-711a-4e5d-8409-b7ce60b08858
keywords:
- AdapterControl ルーチンを設定します。
- 書き込みの AdapterControl ルーチン
- アダプター オブジェクトの WDK カーネル、AdapterControl ルーチンを記述
- AdapterControl ルーチンを記述、DMA 転送 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37c992d6f2088e3f63faa1cc949e35eaaaa3c84c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360262"
---
# <a name="setting-up-adaptercontrol-routines"></a>AdapterControl ルーチンのセットアップ





PnP ドライバーのディスパッチ ルーチン[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求が、次を実行する必要があります、 [ *AdapterControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_control)ルーチン。

1.  入力することでデバイスの DMA の機能のアダプタ オブジェクトを設定、 [**デバイス\_説明**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_description)構造と通話[ **IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter).

2.  アダプター オブジェクトへのポインターを保存し、 *NumberOfMapRegisters*によって返される**IoGetDmaAdapter**します。

    プラットフォーム固有の最大*NumberOfMapRegisters*によって返される**IoGetDmaAdapter**またはドライバーのデバイスの転送機能、方制限が厳しい、決定かどうか、ドライバーは、特定の転送要求を分割し、その IRP を満たすために、そのデバイス上の 1 つ以上の DMA 操作を実行する必要があります。

返されるアダプター オブジェクトへのポインター、ドライバーのエントリ ポイント*AdapterControl* 、ルーチン、*デバイス オブジェクト*ポインターの現在の IRP では、ターゲット デバイスを表す、*コンテキスト*用に既に設定領域へのポインター、 *AdapterControl*ルーチン、および*NumberOfMapRegisters*上限値より小さいなる値の数より小さい要求の転送への呼び出しで渡す必要がある[ **AllocateAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_adapter_channel)します。 通常、ドライバーの[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio) (または場合によって[ *ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049)) ルーチンがある領域を設定*コンテキスト*を呼び出す前に**AllocateAdapterChannel**します。

 

 




