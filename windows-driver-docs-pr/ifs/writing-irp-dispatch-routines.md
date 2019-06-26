---
title: IRP ディスパッチ ルーチンの記述
description: IRP ディスパッチ ルーチンの記述
ms.assetid: 8ce88932-cba6-4261-a938-d38133c20355
keywords:
- フィルター ドライバー WDK ファイル システム、IRP ディスパッチ ルーチン
- ファイル システム フィルター ドライバー WDK、IRP ディスパッチ ルーチン
- ディスパッチ ルーチン WDK ファイル システム
- IRP ディスパッチ ルーチン WDK ファイル システム
- IRP ディスパッチ ルーチンを記述
- IRP ディスパッチ ルーチン WDK ファイル システム、IRP ディスパッチ ルーチンを記述する方法
- Irp WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6088b666e17302512cc3ef6b639f67111dc0e517
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385648"
---
# <a name="writing-irp-dispatch-routines"></a>IRP ディスパッチ ルーチンの記述


## <span id="ddk_writing_irp_dispatch_routines_if"></span><span id="DDK_WRITING_IRP_DISPATCH_ROUTINES_IF"></span>


<div class="alert">
<strong>注</strong>最適な信頼性とパフォーマンスは、使用はお勧め<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">ファイル システム ミニフィルター ドライバー</a>従来のファイル システム フィルター ドライバーの代わりにします。 また、従来のファイル システム フィルター ドライバーは、directaccess (DAX) ボリュームにアタッチできません。 詳細については、ファイル システム ミニフィルター ドライバーは、次を参照してください。<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">フィルター マネージャー モデルの利点</a>します。 ミニフィルター ドライバーは従来、ドライバーを移植するには、次を参照してください。<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">レガシ フィルター ドライバーを移植するためのガイドライン</a>します。
</div>
 

ファイル システム フィルター ドライバーは、デバイス ドライバーで使用されているようなディスパッチ ルーチンを使用します。 A*ディスパッチ ルーチン*Irp の 1 つまたは複数の種類を処理します。 (、*型*IRP は、主要な関数のコードによって決定されます)。ドライバーの[DriverEntry](initializing-a-file-system-filter-driver.md)ルーチン*登録*ドライバー オブジェクトのディスパッチ テーブルに保存して日常的なエントリ ポイントをディスパッチします。 IRP がドライバーに送信されると、I/O サブシステムは IRP の主要な関数のコードに基づく適切なディスパッチ ルーチンを呼び出します。

すべての IRP ディスパッチ ルーチンの定義は次のとおりです。

```cpp
NTSTATUS 
(*PDRIVER_DISPATCH) ( 
    IN PDEVICE_OBJECT DeviceObject, 
    IN PIRP Irp 
    ); 
```

ファイル システム フィルター ドライバーのディスパッチ ルーチンは、IRQL パッシブに最も多くの場合、呼び出されます。\_レベル、ユーザー モード アプリケーションのスレッドでは通常、I/O 要求を生成したスレッドのコンテキストでします。 ただし、このルールをいくつかの例外もあります。 たとえば、ページ フォールトは読み取りが発生して、IRQL APC 時に呼び出すディスパッチ ルーチンを記述\_レベル。 これらの例外は内のテーブルにまとめます[ディスパッチ日常的な IRQL とスレッドのコンテキスト](dispatch-routine-irql-and-thread-context.md)します。 残念ながら、現時点フィルター チェーン内のドライバーの呼び出しを防止することはない[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) IRQL で&gt;パッシブ\_レベル (たとえばに障害が発生しました。リリース spinlock または高速なミュー テックス)。 それにもかかわらず、強くお勧めルーチンが常に呼び出し、そのフィルター ディスパッチ**保留**呼び出される位置同じ IRQL でします。

ディスパッチ ルーチンにできるページング可能なで説明する条件を満たす場合、[ドライバー ページングを行う](https://docs.microsoft.com/windows-hardware/drivers/kernel/making-drivers-pageable)カーネル モード ドライバーのアーキテクチャの設計ガイドの「します。

ファイル システム フィルター ドライバーに制御デバイス オブジェクト (CDO) がある場合は、そのディスパッチ ルーチンを検出し、IRP のターゲット デバイス オブジェクトが、マウントされたボリュームのボリューム デバイス オブジェクト (提供) ではなく、CDO である場合の処理である必要があります。 詳細については、CDO を参照してください。[フィルター ドライバーの制御デバイス オブジェクト](the-filter-driver-s-control-device-object.md)します。

このセクションでは、次のトピックについて説明します。

[IRP の完了](completing-the-irp.md)

[下位レベルのドライバーに IRP を渡す](passing-the-irp-down-to-lower-level-drivers.md)

[ディスパッチ ルーチンから状態を返す](returning-status-from-dispatch-routines.md)

[例:完了ルーチンを設定せず、IRP を渡す](example--passing-the-irp-down-without-setting-a-completion-routine.md)

[ディスパッチ ルーチンの制約](constraints-on-dispatch-routines.md)

[ディスパッチの日常的な IRQL とスレッドのコンテキスト](dispatch-routine-irql-and-thread-context.md)

 

 




