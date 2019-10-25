---
title: IRP ディスパッチルーチンの記述
description: IRP ディスパッチルーチンの記述
ms.assetid: 8ce88932-cba6-4261-a938-d38133c20355
keywords:
- フィルタードライバー WDK ファイルシステム、IRP ディスパッチルーチン
- ファイルシステムフィルタードライバー WDK、IRP ディスパッチルーチン
- ディスパッチルーチン WDK ファイルシステム
- IRP ディスパッチルーチン WDK ファイルシステム
- IRP ディスパッチルーチンの記述
- IRP ディスパッチルーチン WDK ファイルシステム、IRP ディスパッチルーチンの記述について
- Irp WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b3f5128c8b133858d14c514627d849dab3756d3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840922"
---
# <a name="writing-irp-dispatch-routines"></a>IRP ディスパッチルーチンの記述


## <span id="ddk_writing_irp_dispatch_routines_if"></span><span id="DDK_WRITING_IRP_DISPATCH_ROUTINES_IF"></span>


<div class="alert">
<strong>メモ</strong>  最適な信頼性とパフォーマンスを得るには、従来のファイルシステムフィルタードライバーではなく、<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">ファイルシステムミニフィルタードライバー</a>を使用することをお勧めします。 また、レガシファイルシステムフィルタードライバーは、直接アクセス (DAX) ボリュームにアタッチできません。 ファイルシステムミニフィルタードライバーの詳細については、「<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">フィルターマネージャーモデルの利点</a>」を参照してください。 レガシドライバーをミニフィルタードライバーに移植する方法については、「<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">レガシフィルタードライバーを移植するためのガイドライン</a>」を参照してください。
</div>
 

ファイルシステムフィルタードライバーは、デバイスドライバーで使用されるものと似たディスパッチルーチンを使用します。 *ディスパッチルーチン*は、1つまたは複数の種類の irp を処理します。 (IRP の*種類*は、主要な関数コードによって決まります)。ドライバーの[driverentry](initializing-a-file-system-filter-driver.md)ルーチンは、ディスパッチルーチンのエントリポイントをドライバーオブジェクトのディスパッチテーブルに格納することによって*登録*します。 IRP がドライバーに送信されると、i/o サブシステムは、IRP の主要な関数コードに基づいて適切なディスパッチルーチンを呼び出します。

各 IRP ディスパッチルーチンは、次のように定義されます。

```cpp
NTSTATUS 
(*PDRIVER_DISPATCH) ( 
    IN PDEVICE_OBJECT DeviceObject, 
    IN PIRP Irp 
    ); 
```

ファイルシステムフィルタードライバーのディスパッチルーチンは、通常、i/o 要求を発生させたスレッドのコンテキスト (通常はユーザーモードのアプリケーションスレッド) で、IRQL パッシブ\_レベルで呼び出されます。 ただし、このルールにはいくつかの例外があります。 たとえば、ページフォールトが発生すると、読み取りおよび書き込みのディスパッチルーチンが IRQL APC\_レベルで呼び出されます。 これらの例外は、[ディスパッチルーチンの IRQL とスレッドコンテキスト](dispatch-routine-irql-and-thread-context.md)の表にまとめられています。 残念ながら、現時点では、フィルターチェーン内のドライバーによって、&gt; パッシブ\_レベル (たとえば、スピンロックや高速ミューテックスの解放に失敗した場合など) に[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)が呼び出されないようにすることはできません。 ただし、フィルターディスパッチルーチンは、呼び出されたのと同じ IRQL で常に**IoCallDriver**を呼び出すことを強くお勧めします。

ディスパッチルーチンは、カーネルモードドライバーアーキテクチャ設計ガイドの「[ドライバーのページング](https://docs.microsoft.com/windows-hardware/drivers/kernel/making-drivers-pageable)を変更する」セクションで説明されている条件を満たす場合に、ページング可能にすることができます。

ファイルシステムフィルタードライバーにコントロールデバイスオブジェクト (CDO) がある場合、そのディスパッチルーチンは、IRP のターゲットデバイスオブジェクトが、マウントされたボリュームのボリュームデバイスオブジェクト (VDO) ではなく、CDO であるケースを検出して処理できる必要があります。 CDO の詳細については、[フィルタードライバーのコントロールデバイスオブジェクトに](the-filter-driver-s-control-device-object.md)関する説明を参照してください。

このセクションでは、次のトピックについて説明します。

[IRP の完了](completing-the-irp.md)

[IRP を下位レベルのドライバーに渡す](passing-the-irp-down-to-lower-level-drivers.md)

[ディスパッチルーチンから状態を返す](returning-status-from-dispatch-routines.md)

[例: 完了ルーチンを設定せずに IRP を渡す](example--passing-the-irp-down-without-setting-a-completion-routine.md)

[ディスパッチルーチンの制約](constraints-on-dispatch-routines.md)

[ディスパッチルーチンの IRQL とスレッドコンテキスト](dispatch-routine-irql-and-thread-context.md)

 

 




