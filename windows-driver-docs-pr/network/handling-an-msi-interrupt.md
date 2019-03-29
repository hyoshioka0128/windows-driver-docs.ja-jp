---
title: MSI 割り込みの処理
description: MSI 割り込みの処理
ms.assetid: c8e2a5a4-17f5-48a3-a2d0-6eca2a0b7f45
keywords:
- MSI X WDK ネットワーク、割り込み処理
- メッセージ シグナル割り込み WDK ネットワー キング、割り込み処理
- Msi WDK ネットワー キング、割り込み処理
- WDK ネットワーク、処理を中断します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c412d56e597e0c2c8b0391d471c0ac42169f7572
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573731"
---
# <a name="handling-an-msi-interrupt"></a>MSI 割り込みの処理





NDIS 呼び出し、 [ *MiniportMessageInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff559407)ネットワーク インターフェイス カード (NIC) は、割り込みを生成するときに機能します。 *MessageId* MSI X メッセージがこの関数のパラメーターを識別します。

*MiniportMessageInterrupt*常に返す必要があります**TRUE**メッセージ割り込みが共有されていないため、割り込みを処理した後。

ミニポート ドライバーで可能な限り少量の作業を行う必要があります、 *MiniportMessageInterrupt*関数。 ドライバーは、I/O 操作を延期する必要があります、 [ *MiniportMessageInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff559411) NDIS は、割り込みの遅延の処理を完了するために呼び出す関数。

その他のキューに遅延プロシージャ呼び出し (Dpc) の後[ *MiniportMessageInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff559407) 、ミニポート ドライバーのビットのセットを返します、 *TargetProcessors*パラメーター、 *MiniportMessageInterrupt*関数。 要求から追加 Dpc *MiniportMessageInterrupt*または*MiniportMessageInterruptDPC*、ミニポート ドライバーを呼び出すことができます、 [ **NdisMQueueDpc**](https://msdn.microsoft.com/library/windows/hardware/ff563637)関数。

ミニポート ドライバーを呼び出すことができます**NdisMQueueDpc**を他のプロセッサの Dpc が追加を要求します。

NDIS 6.1 と以降のバージョンに必ず Dpc の同じ CPU が個別にキューにスケジュールされている別のメッセージ。 たとえば、ミニポート ドライバーでは、CPU 1 (1 つの DPC メッセージを格納およびメッセージ 1 の他の DPC) を同時に 2 つの Dpc をスケジュールする場合、2 つの Dpc は CPU 1 (メッセージ 0 と 1 つの DPC) およびメッセージ 1 と他の DPC キューに配置します。

NDIS は、異なる Cpu でスケジュールされている、同じメッセージの Dpc のキューは別々 にも保証されます。 たとえば、ミニポート ドライバーのスケジュール (1 つのメッセージ 0 の場合は 0 を CPU で DPC) と 1 つの DPC メッセージ 0 を CPU 1、2 つの Dpc は、2 つの個別 Dpc が CPU 0 および CPU 1、0 のメッセージの両方にキューイングされます。

 

 





