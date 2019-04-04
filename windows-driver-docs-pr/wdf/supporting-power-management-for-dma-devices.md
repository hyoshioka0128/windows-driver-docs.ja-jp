---
title: DMA デバイスの電源管理をサポートしています。
description: DMA デバイスの電源管理をサポートしています。
ms.assetid: abbb8f60-560f-41c9-85c5-1ec82078b99e
keywords:
- DMA 操作 WDK KMDF、電源管理
- バス マスター DMA WDK KMDF、電源管理
- 電源管理 WDK KMDF、DMA デバイス
- DMA イネーブラー オブジェクト WDK KMDF
- WDK KMDF のオブジェクトの有効化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b51108cd48db25de18192183ff2f1831fe5769e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527875"
---
# <a name="supporting-power-management-for-dma-devices"></a>DMA デバイスの電源管理をサポートしています。


\[KMDF にのみ適用されます。\]

DMA イネーブラー オブジェクトでは、DMA デバイス用のドライバーに、およびデバイスの操作 (D0) 状態からの移行を管理に使用できる省略可能なイベントのコールバック関数のセットを定義します。

DMA デバイスは、州、およびフレームワークの後にその作業を入力するたびに、ドライバーが呼び出されて[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)コールバック関数では、フレームワークが呼び出す DMA コールバック関数を次に、一覧の順序:

<a href="" id="---------evtdmaenablerfill--------"></a>[*EvtDmaEnablerFill*](https://msdn.microsoft.com/library/windows/hardware/ff540932)  
デバイスの DMA バッファーを割り当てます。

<a href="" id="---------evtdmaenablerenable--------"></a>[*EvtDmaEnablerEnable*](https://msdn.microsoft.com/library/windows/hardware/ff540929)  
デバイスの作業 (D0) 状態に入った後は、デバイスの DMA の機能を有効にします。

<a href="" id="---------evtdmaenablerselfmanagediostart--------"></a>[*EvtDmaEnablerSelfManagedIoStart*](https://msdn.microsoft.com/library/windows/hardware/ff541663)  
DMA デバイスの自己管理型の I/O 操作を開始します。

州、およびフレームワークの前に、DMA デバイスがその作業を離れるたびに、ドライバーが呼び出されて[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)コールバック関数では、フレームワークが呼び出す DMA コールバック関数を次に、一覧の順序:

<a href="" id="---------evtdmaenablerselfmanagediostop--------"></a>[*EvtDmaEnablerSelfManagedIoStop*](https://msdn.microsoft.com/library/windows/hardware/ff541677)  
DMA デバイスの自己管理型の I/O 操作を停止します。

<a href="" id="---------evtdmaenablerdisable--------"></a>[*EvtDmaEnablerDisable*](https://msdn.microsoft.com/library/windows/hardware/ff540927)  
デバイスがその作業 (D0) 状態を抜ける前に、デバイスの DMA の機能を無効にします。

<a href="" id="---------evtdmaenablerflush--------"></a>[*EvtDmaEnablerFlush*](https://msdn.microsoft.com/library/windows/hardware/ff541655)  
デバイスの DMA バッファーの割り当てを解除します。

これで、フレームワーク ドライバーのイベントのコールバック関数、順序の詳細については、[PnP および電源管理のシナリオ](pnp-and-power-management-scenarios.md)を参照してください。

 

 





