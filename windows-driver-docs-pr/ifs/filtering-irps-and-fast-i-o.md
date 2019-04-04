---
title: Irp と高速な I/O をフィルター処理
description: Irp と高速な I/O をフィルター処理
ms.assetid: fad124b0-525d-4ff9-8f2c-3817fc76685c
keywords:
- フィルター ドライバー WDK のファイル システム、IRP がフィルター処理
- ファイル システム フィルター ドライバー WDK、IRP がフィルター処理
- Irp WDK ファイル システム
- Irp WDK ファイル システムをフィルター処理
- 高速の I/O の WDK ファイル システムをフィルター処理
- WDK のファイル システムをフィルター処理、高速な I/O
- ファイル システムの I/O の WDK
- ディスパッチ ルーチン WDK ファイル システム
- I/O 要求の WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84b309bdb20036e4d89a7cd2b6df275bddcd3df3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550129"
---
# <a name="filtering-irps-and-fast-io"></a>Irp と高速な I/O をフィルター処理


## <span id="ddk_filtering_irps_and_fast_io_if"></span><span id="DDK_FILTERING_IRPS_AND_FAST_IO_IF"></span>


<div class="alert">
<strong>注</strong>最適な信頼性とパフォーマンスは、使用はお勧め<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">ファイル システム ミニフィルター ドライバー</a>従来のファイル システム フィルター ドライバーの代わりにします。 また、従来のファイル システム フィルター ドライバーは、directaccess (DAX) ボリュームにアタッチできません。 詳細については、ファイル システム ミニフィルター ドライバーは、<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">フィルター マネージャー モデルの利点</a>を参照してください。 ミニフィルター ドライバーは従来、ドライバーを移植するには、<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">レガシ フィルター ドライバーを移植するためのガイドライン</a>を参照してください。
</div>
 

ファイル システム フィルター ドライバーは、ファイル システムまたはファイル システム ボリュームの 1 つまたは複数の I/O 要求をフィルター処理します。 I/O 要求ごとでは、I/O 要求パケット (IRP) または高速の I/O 要求が表示されます。 Irp は、ドライバーの IRP ディスパッチ ルーチンによって処理される I/O システム構造です。 高速の I/O 要求は、ドライバーの高速な I/O コールバック ルーチンによって処理されます。

フィルター ドライバーが初期化されると、その**DriverEntry**ルーチンが、フィルター ドライバーの IRP ディスパッチ ルーチンおよび高速の I/O コールバック ルーチンを登録します。 フィルター ドライバーごとにこれらのルーチンのセットを 1 つだけを登録することができます。

Irp の種類によって、高速の I/O 対応していくつかの高速の I/O 要求 IRP の相当します。 ただし、Irp がさまざまな種類の高速な I/O できません I/O を処理します。 また、特定の特殊化された高速な I/O ルーチンは、IRP を作成しなくても、キャッシュ マネージャーまたはメモリ マネージャーのファイル システム リソースを preacquire に使用されます。 そのため、ほとんどの場合、Irp や高速の I/O 要求で実行する個別のロールの I/O 操作。

このセクションでは、次のトピックについて説明します。

[Irp が高速な I/O によって異なる](irps-are-different-from-fast-i-o.md)

[ファイル システム フィルター ドライバーのデバイス オブジェクトの種類](types-of-device-objects-used-by-file-system-filter-drivers.md)

 

 




