---
title: ディスパッチ ルーチンから返される状態
description: ディスパッチ ルーチンから返される状態
ms.assetid: 76bd651a-344f-4e22-a435-b62fdf2d7ddc
keywords:
- IRP ディスパッチ ルーチン WDK ファイル システムの状態の取得
- 状態値 WDK ファイル システム
- 成功状態の値の WDK ファイル システム
- WDK のファイル システムの状態を返す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea021e58d61e949c1a44645084d8f1c5a07e1ee9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385938"
---
# <a name="returning-status-from-dispatch-routines"></a>ディスパッチ ルーチンから返される状態


## <span id="ddk_returning_status_from_dispatch_routines_if"></span><span id="DDK_RETURNING_STATUS_FROM_DISPATCH_ROUTINES_IF"></span>


ディスパッチ ルーチン完了ルーチンが設定されていないことがによって返される NTSTATUS 値を返す必要があります常に IRP を完了したときに点を除いて[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)します。 この値が状態でない限り\_、保留中の値に一致する必要があります**Irp -&gt;IoStatus.Status** IRP の完了したドライバーで設定します。

次のいずれかの作業キューに IRP を投稿する可能性があります完了ルーチンを設定するディスパッチ ルーチンを実行してください。

-   によって返された NTSTATUS 値を返す**保留**します。

-   イベントを通知し、値を返す完了ルーチンの待機**Irp -&gt;IoStatus.Status**します。

-   保留中の IRP をマーク、ワーク キューに投稿、および状態を返す\_保留します。

-   ディスパッチ ルーチンが保留中の IRP をマークする必要があり、状態を返す完了ルーチンでは、作業キューに IRP を post 可能性がある場合、\_保留します。

これらの動作が正しいこと、またはこともできます、特定の操作に依存します。 ディレクトリ変更の通知など、いくつかの操作を同期的です。 にすることはできません。非同期の各 oplock など、一部にすることはできません。

ディスパッチ ルーチンから状態を返す方法についての詳細については、次を参照してください。[ディスパッチ ルーチンに対する制約](constraints-on-dispatch-routines.md)します。

 

 




