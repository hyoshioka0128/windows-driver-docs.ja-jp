---
title: IRP 完了ルーチンの使用
description: IRP 完了ルーチンの使用
ms.assetid: 82b9ba2b-17db-40e5-be3f-fd77cd986781
keywords:
- フィルター ドライバー WDK ファイル システム、IRP の完了ルーチン
- ファイル システム フィルター ドライバー WDK、IRP の完了ルーチン
- IRP の完了ルーチン WDK ファイル システム
- Irp WDK ファイル システム
- WDK のファイル システムを要求する I/O の完了
- IRP の完了ルーチン WDK IRP の完了ルーチンの詳細については、システムをファイルします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed82fa6e50c103aefc06e53b444e695109af9a2e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380278"
---
# <a name="using-irp-completion-routines"></a>IRP 完了ルーチンの使用


## <span id="ddk_using_irp_completion_routines_if"></span><span id="DDK_USING_IRP_COMPLETION_ROUTINES_IF"></span>


<div class="alert">
<strong>注</strong>最適な信頼性とパフォーマンスは、使用はお勧め<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">ファイル システム ミニフィルター ドライバー</a>従来のファイル システム フィルター ドライバーの代わりにします。 また、従来のファイル システム フィルター ドライバーは、directaccess (DAX) ボリュームにアタッチできません。 詳細については、ファイル システム ミニフィルター ドライバーは、次を参照してください。<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">フィルター マネージャー モデルの利点</a>します。 ミニフィルター ドライバーは従来、ドライバーを移植するには、次を参照してください。<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">レガシ フィルター ドライバーを移植するためのガイドライン</a>します。
</div>
 

ファイル システム フィルター ドライバーは、デバイス ドライバーで使用されるものに類似した完了ルーチンを使用します。 A*完了ルーチン*完了 IRP の処理を実行します。 [次へ] の下位レベルのドライバーは IRP を通過するドライバーのルーチンは呼び出すことによって IRP の完了ルーチンを必要に応じて登録できます[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)呼び出す前に[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)します。

すべて IRP の完了ルーチンの定義は次のとおりです。

```cpp
NTSTATUS 
(*PIO_COMPLETION_ROUTINE) ( 
    IN PDEVICE_OBJECT DeviceObject, 
    IN PIRP Irp, 
    IN PVOID Context 
    ); 
```

完了のルーチンは IRQL で呼び出される&lt;= ディスパッチ\_レベルを任意のスレッド コンテキスト。

IRQL のディスパッチで呼び出すことができるため、\_レベル、完了ルーチンは、下の IRQL でなど、呼び出す必要があるカーネル モードのルーチンを呼び出すことはできません[ **IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)します。 同じ理由で完了ルーチンで使用されている任意のデータ構造は、非ページ プールから割り当てる必要があります。

このセクションでは、次のトピックについて説明します。

[完了処理を実行する方法](how-completion-processing-is-performed.md)

[PendingReturned フラグのチェック](checking-the-pendingreturned-flag.md)

[完了ルーチンから状態を返す](returning-status-from-completion-routines.md)

[例:単純なパススルー ディスパッチと完了](example--simple-pass-through-dispatch-and-completion.md)

[完了ルーチンの制約](constraints-on-completion-routines.md)

 

 




