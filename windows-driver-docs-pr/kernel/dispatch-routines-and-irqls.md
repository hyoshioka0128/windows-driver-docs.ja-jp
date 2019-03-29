---
title: ディスパッチ ルーチンと IRQL
description: ディスパッチ ルーチンと IRQL
ms.assetid: fe64e0f7-3906-470a-86c5-03460e652eed
keywords:
- ルーチンの WDK カーネル、Irql をディスパッチします。
- Irql WDK ディスパッチ ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb9821d992fe0db9cc18b18e5a2448e0e9908f65
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573547"
---
# <a name="dispatch-routines-and-irqls"></a>ディスパッチ ルーチンと IRQL





ほとんどのドライバーのディスパッチ ルーチンは IRQL で任意のスレッド コンテキストで呼び出されます。 パッシブ =\_レベルで、次の例外。

-   最上位レベルのドライバーのディスパッチ ルーチンは、ユーザー モード アプリケーションのスレッドでは通常、I/O 要求を生成したスレッドのコンテキストで呼び出されます。

    つまり、ファイル システム ドライバーと他の最上位レベルのドライバーのディスパッチ ルーチンが、IRQL で nonarbitrary スレッド コンテキストで呼びます。 パッシブ =\_レベル。

-   [ *DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)、 [ *DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)、および[ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch) IRQL で最下位レベルのデバイス ドライバー、およびシステムのページング パスでそれらの上に配置する中間のドライバーのルーチンを呼び出すことができます = APC\_レベルと任意のスレッド コンテキストでします。

    *DispatchRead*や*DispatchWrite*ルーチン、およびその他のルーチンもプロセスの読み取りや書き込み要求をそれらの最下位レベルのデバイスや中間のドライバーである必要があります常駐まったく時間。 これらのドライバー ルーチンはページング可能などちらもページング可能なイメージのドライバーの一部にするセクション。ページング可能なメモリにアクセスする必要がありますされません。 さらに、することはできません、ブロッキング呼び出しに依存 (など[ **kewaitforsingleobject の 1** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)タイムアウトは 0 以外の場合)。

-   [ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch) IRQL で休止状態やページング パス内のドライバーのルーチンを呼び出すことができます = ディスパッチ\_レベル。 [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch) PnP を処理するためにこのようなドライバーのルーチンを準備する必要があります[ **IRP\_MN\_デバイス\_使用状況\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff550841)要求。

-   *DispatchPower* IRQL で起動時に突入パワーが必要なドライバーのルーチンを呼び出すことができます = ディスパッチ\_レベル。

詳細については、次を参照してください。[を管理するハードウェアの優先順位](managing-hardware-priorities.md)します。

 

 




