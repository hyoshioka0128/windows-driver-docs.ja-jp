---
title: IRP ディスパッチ ルーチンの記述
description: IRP ディスパッチ ルーチンの記述
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
ms.openlocfilehash: 0cd694852f16cb242e427cb3ccc9e3ce8844e0f9
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910441"
---
# <a name="writing-irp-dispatch-routines"></a>IRP ディスパッチ ルーチンの記述

> [!NOTE]
> 最適な信頼性とパフォーマンスを得るには、従来のファイルシステムフィルタードライバーではなく、フィルターマネージャーをサポートする[ファイルシステムミニフィルタードライバー](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-concepts)を使用します。 レガシドライバーをミニフィルタードライバーに移植する方法については、「[レガシフィルタードライバーを移植するためのガイドライン](guidelines-for-porting-legacy-filter-drivers.md)」を参照してください。

ファイルシステムフィルタードライバーは、デバイスドライバーで使用されるものと似たディスパッチルーチンを使用します。 *ディスパッチルーチン*は、1つまたは複数の種類の irp を処理します。 (IRP の*種類*は、主要な関数コードによって決まります)。ドライバーの[driverentry](initializing-a-file-system-filter-driver.md)ルーチンは、ディスパッチルーチンのエントリポイントをドライバーオブジェクトのディスパッチテーブルに格納することによって*登録*します。 IRP がドライバーに送信されると、i/o サブシステムは、IRP の主要な関数コードに基づいて適切なディスパッチルーチンを呼び出します。

各 IRP ディスパッチルーチンは、次のように定義されます。

```cpp
NTSTATUS
(*PDRIVER_DISPATCH) (
    IN PDEVICE_OBJECT DeviceObject,
    IN PIRP Irp
    );
```

ファイルシステムフィルタードライバーのディスパッチルーチンは、通常、ユーザーモードのアプリケーションスレッドである i/o 要求を発生させたスレッドのコンテキストで、IRQL PASSIVE_LEVEL で呼び出されます。 ただし、このルールにはいくつかの例外があります。 たとえば、ページフォールトでは、読み取りおよび書き込みのディスパッチルーチンが IRQL APC_LEVEL で呼び出されます。 これらの例外は、[ディスパッチルーチンの IRQL とスレッドコンテキスト](dispatch-routine-irql-and-thread-context.md)の表にまとめられています。 残念ながら、現時点では、フィルターチェーンのドライバーが IRQL > PASSIVE_LEVEL で[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出さないようにすることはできません (たとえば、スピンロックや高速ミューテックスの解放に失敗するなど)。 ただし、フィルターディスパッチルーチンは、呼び出されたのと同じ IRQL で常に**IoCallDriver**を呼び出すことを強くお勧めします。

ディスパッチルーチンは、カーネルモードドライバーアーキテクチャ設計ガイドの「[ドライバーのページング](https://docs.microsoft.com/windows-hardware/drivers/kernel/making-drivers-pageable)を変更する」セクションで説明されている条件を満たす場合に、ページング可能にすることができます。

ファイルシステムフィルタードライバーにコントロールデバイスオブジェクト (CDO) がある場合、そのディスパッチルーチンは、IRP のターゲットデバイスオブジェクトが、マウントされたボリュームのボリュームデバイスオブジェクト (VDO) ではなく、CDO であるケースを検出して処理できる必要があります。 CDO の詳細については、[フィルタードライバーのコントロールデバイスオブジェクトに](the-filter-driver-s-control-device-object.md)関する説明を参照してください。

このセクションでは、次のトピックについて説明します。

[IRP の完了](completing-the-irp.md)

[IRP を下位レベルのドライバーに渡す](passing-the-irp-down-to-lower-level-drivers.md)

[ディスパッチルーチンから状態を返す](returning-status-from-dispatch-routines.md)

[例: 完了ルーチンを設定せずに IRP を渡す](example--passing-the-irp-down-without-setting-a-completion-routine.md)

[ディスパッチルーチンの制約](constraints-on-dispatch-routines.md)

[ディスパッチルーチンの IRQL とスレッドコンテキスト](dispatch-routine-irql-and-thread-context.md)
