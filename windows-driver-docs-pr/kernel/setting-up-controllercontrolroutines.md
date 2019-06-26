---
title: ControllerControl ルーチンのセットアップ
description: ControllerControl ルーチンのセットアップ
ms.assetid: 007247c1-b51e-4677-9a46-78ff9f1c8996
keywords:
- コント ローラー オブジェクトの WDK カーネル、ControllerControl ルーチンを記述
- 書き込みの ControllerControl ルーチン
- ControllerControl ルーチンを設定します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf65cdb54c6599ae2f265f66a39a49a89551b4b7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383025"
---
# <a name="setting-up-controllercontrol-routines"></a>ControllerControl ルーチンのセットアップ





ドライバーの[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンは、受信すると、次に行う必要があります、 [ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)を設定する、要求、 [ *ControllerControl* ](https://msdn.microsoft.com/library/windows/hardware/ff542049)ルーチン。

1.  呼び出す[ **IoCreateController** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatecontroller)ドライバー決定を指定する、コント ローラー オブジェクトを設定する*サイズ*から、システムによって割り当てられたコント ローラー拡張機能非ページ プールとゼロで初期化します。

2.  保存、 *ControllerObject*によって返されたポインター **IoCreateController**、ハードウェアによって制御される論理または物理デバイスを表す各デバイス オブジェクトのデバイスの拡張機能では、通常コント ローラーのオブジェクトによって表されます。

3.  セットアップや初期化のドライバーにより決定された内容、* ControllerObject * **-&gt;ControllerExtension**します。

返された*ControllerObject*ポインター、ドライバーのエントリ ポイント*ControllerControl* 、ルーチン、*デバイス オブジェクト*のターゲット デバイスを表すポインター現在の IRP では、および*コンテキスト*用に既に設定領域へのポインター、 *ControllerControl*ルーチンは、ドライバーの呼び出しで渡す必要がある[ **IoAllocateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioallocatecontroller)します。 通常、ドライバーの[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチンがある領域を設定*コンテキスト*を呼び出す前に**IoAllocateController**します。

 

 




