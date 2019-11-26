---
title: ドライバーの状態の確認エラー
description: ドライバーの状態の確認エラー
ms.assetid: 963f79f6-2282-41bd-9cf4-bd5bc02a510e
keywords:
- 信頼性 WDK カーネル、ドライバーの状態チェック
- ドライバーの状態の確認
- ドライバーの状態の確認
- ドライバーの状態の確認
- 正しいデバイスの状態 WDK カーネル
- 'デバイスの状態: WDK カーネル'
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2f67b5b97a2eae9fdba1545fd1c6586cc25b8c6
ms.sourcegitcommit: 01bcf26722f1a51d2b5ebcdcbc08518b3ee08474
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74308544"
---
# <a name="failure-to-check-a-drivers-state"></a>ドライバーの状態の確認エラー





次の例では、ドライバーは**ASSERT**マクロを使用して、ドライバーイメージのデバッグバージョンで正しいデバイスの状態を確認しますが、同じドライバーソースのリテールビルドではデバイスの状態を確認しません。

```cpp
   case IOCTL_WAIT_FOR_EVENT:

      ASSERT((!Extension->WaitEventIrp));
      Extension->WaitEventIrp = Irp;
      IoMarkIrpPending(Irp);
      status = STATUS_PENDING;
```

デバッグドライバーのイメージでは、ドライバーが保留中の IRP を既に保持している場合、システムはをアサートします。 ただし、リテールビルドでは、ドライバーはこのエラーをチェックしません。 同じ IOCTL の2つの呼び出しにより、ドライバーが IRP を追跡しなくなります。

マルチプロセッサシステムでは、このコード片によって追加の問題が発生する可能性があります。 このルーチンには、この IRP の所有権 (操作する権利) があることを前提としています。 ルーチンが**irp**ポインターを**拡張&gt;WaitEventIrp**のグローバル構造に保存すると、別のスレッドがそのグローバル構造から irp アドレスを取得し、irp に対して操作を実行できるようになります。 この問題を回避するには、ドライバーは irp を保存する前に保留中の IRP をマークし、 [**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)の呼び出しと、インタロックされたシーケンス内の割り当ての両方を含める必要があります。 また、IRP の[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンが必要になる場合もあります。

 

 




