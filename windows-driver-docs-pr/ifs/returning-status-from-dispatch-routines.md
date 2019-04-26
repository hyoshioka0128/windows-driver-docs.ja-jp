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
ms.openlocfilehash: 4c08527fb47b9a81d22804867a6d2157563392e2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344543"
---
# <a name="returning-status-from-dispatch-routines"></a>ディスパッチ ルーチンから返される状態


## <span id="ddk_returning_status_from_dispatch_routines_if"></span><span id="DDK_RETURNING_STATUS_FROM_DISPATCH_ROUTINES_IF"></span>


ディスパッチ ルーチン完了ルーチンが設定されていないことがによって返される NTSTATUS 値を返す必要があります常に IRP を完了したときに点を除いて[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)します。 この値が状態でない限り\_、保留中の値に一致する必要があります**Irp -&gt;IoStatus.Status** IRP の完了したドライバーで設定します。

次のいずれかの作業キューに IRP を投稿する可能性があります完了ルーチンを設定するディスパッチ ルーチンを実行してください。

-   によって返された NTSTATUS 値を返す**保留**します。

-   イベントを通知し、値を返す完了ルーチンの待機**Irp -&gt;IoStatus.Status**します。

-   保留中の IRP をマーク、ワーク キューに投稿、および状態を返す\_保留します。

-   ディスパッチ ルーチンが保留中の IRP をマークする必要があり、状態を返す完了ルーチンでは、作業キューに IRP を post 可能性がある場合、\_保留します。

これらの動作が正しいこと、またはこともできます、特定の操作に依存します。 ディレクトリ変更の通知など、いくつかの操作を同期的です。 にすることはできません。非同期の各 oplock など、一部にすることはできません。

ディスパッチ ルーチンから状態を返す方法についての詳細については、次を参照してください。[ディスパッチ ルーチンに対する制約](constraints-on-dispatch-routines.md)します。

 

 




