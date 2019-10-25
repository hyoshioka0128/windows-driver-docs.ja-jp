---
title: IRP 完了ルーチンの使用
description: IRP 完了ルーチンの使用
ms.assetid: 82b9ba2b-17db-40e5-be3f-fd77cd986781
keywords:
- フィルタードライバー WDK ファイルシステム、IRP 完了ルーチン
- ファイルシステムフィルタードライバー WDK、IRP 入力ルーチン
- IRP 完了ルーチン WDK ファイルシステム
- Irp WDK ファイルシステム
- i/o 要求の完了 (WDK ファイルシステム)
- IRP 完了ルーチン WDK ファイルシステム、IRP 完了ルーチンについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61e2acf0ae6f308b74251c6ad48d76929860f390
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840937"
---
# <a name="using-irp-completion-routines"></a>IRP 完了ルーチンの使用


## <span id="ddk_using_irp_completion_routines_if"></span><span id="DDK_USING_IRP_COMPLETION_ROUTINES_IF"></span>


<div class="alert">
<strong>メモ</strong>  最適な信頼性とパフォーマンスを得るには、従来のファイルシステムフィルタードライバーではなく、<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">ファイルシステムミニフィルタードライバー</a>を使用することをお勧めします。 また、レガシファイルシステムフィルタードライバーは、直接アクセス (DAX) ボリュームにアタッチできません。 ファイルシステムミニフィルタードライバーの詳細については、「<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">フィルターマネージャーモデルの利点</a>」を参照してください。 レガシドライバーをミニフィルタードライバーに移植する方法については、「<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">レガシフィルタードライバーを移植するためのガイドライン</a>」を参照してください。
</div>
 

ファイルシステムフィルタードライバーは、デバイスドライバーで使用されるものと同様の完了ルーチンを使用します。 *完了ルーチン*は、IRP で完了処理を実行します。 次の下位レベルのドライバーに IRP を渡すドライバールーチンは、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出す前に[**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出すことによって、必要に応じて irp の完了ルーチンを登録できます。

各 IRP 完了ルーチンは、次のように定義されます。

```cpp
NTSTATUS 
(*PIO_COMPLETION_ROUTINE) ( 
    IN PDEVICE_OBJECT DeviceObject, 
    IN PIRP Irp, 
    IN PVOID Context 
    ); 
```

完了ルーチンは、任意のスレッドコンテキストで、IRQL &lt;= ディスパッチ\_レベルで呼び出されます。

これらは IRQL ディスパッチ\_レベルで呼び出すことができるため、完了ルーチンは、 [**Iodeletedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)などの低い IRQL で呼び出す必要があるカーネルモードルーチンを呼び出すことはできません。 同じ理由から、完了ルーチンで使用されるデータ構造は、非ページプールから割り当てられる必要があります。

このセクションでは、次のトピックについて説明します。

[完了処理の実行方法](how-completion-processing-is-performed.md)

[PendingReturned たフラグを確認しています](checking-the-pendingreturned-flag.md)

[完了ルーチンから状態を返す](returning-status-from-completion-routines.md)

[例: 単純なパススルーディスパッチと完了](example--simple-pass-through-dispatch-and-completion.md)

[完了ルーチンの制約](constraints-on-completion-routines.md)

 

 




