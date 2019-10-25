---
title: AdapterControl ルーチンのセットアップ
description: AdapterControl ルーチンのセットアップ
ms.assetid: 0d2add25-711a-4e5d-8409-b7ce60b08858
keywords:
- AdapterControl ルーチン、設定
- AdapterControl ルーチン、書き込み
- アダプタオブジェクト WDK カーネル、AdapterControl ルーチンの記述
- DMA が WDK カーネルを転送し、AdapterControl ルーチンを作成する
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bac0441655c2d251aa8a4035eec3ab034ecbb115
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838423"
---
# <a name="setting-up-adaptercontrol-routines"></a>AdapterControl ルーチンのセットアップ





PnP IRP\_に対して実行されるドライバーのディスパッチルーチンは\_デバイスの要求を[**開始\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device) 、 [*adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)ルーチンに対して次の操作を行う必要があります。

1.  デバイス[ **\_説明**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_description)の構造を入力し、 [**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)を呼び出すことによって、デバイスの DMA 機能のアダプターオブジェクトを設定します。

2.  **IoGetDmaAdapter**によって返されたアダプターオブジェクトポインターと*numberofmapregisters*を保存します。

    **IoGetDmaAdapter**によって返される、またはドライバーのデバイスの転送機能のいずれかが制限されている、プラットフォーム固有の最大*numberofmapregisters*は、ドライバーが特定の転送要求を分割する必要があるかどうかを判断し、その IRP を満たすために、デバイスで複数の DMA 操作を実行します。

返されたアダプターオブジェクトポインターは、ドライバーの*Adaptercontrol*ルーチンのエントリポイントであり、現在の IRP のターゲットデバイスを表す*DeviceObject*ポインターであり、既に設定されている *領域へのコンテキストポインターです。AdapterControl*ルーチンと*Numberofmapregisters*値 (小さい転送要求で可能な最大数よりも小さくなる可能性があります) は、 [**allocateadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)への呼び出しで渡す必要があります。 通常、ドライバーの[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) (または[*コントロール*](https://msdn.microsoft.com/library/windows/hardware/ff542049)) ルーチンは、 **allocateadapterchannel**を呼び出す前に、*コンテキスト*で領域を設定します。

 

 




