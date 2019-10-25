---
title: チェンジャー クラス ドライバーのバージョンの違い
description: チェンジャー クラス ドライバーのバージョンの違い
ms.assetid: 4ae4d1b0-cf2f-4c81-b8ae-3a91fd479a89
keywords:
- チェンジャードライバー WDK storage、クラスドライバー
- storage チェンジャードライバー WDK、クラスドライバー
- クラスドライバー WDK storage、チェンジャードライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0202d048b821ea8fc0f08ccfa701e8b94311bc1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845175"
---
# <a name="differences-in-changer-class-driver-versions"></a>チェンジャー クラス ドライバーのバージョンの違い


## <span id="ddk_differences_in_changer_class_driver_versions_kg"></span><span id="DDK_DIFFERENCES_IN_CHANGER_CLASS_DRIVER_VERSIONS_KG"></span>


Windows XP と Windows 2000 のチェンジャークラス/miniclass ドライバーペアの実装には、次の3つの重要な違いがあります。

1.  Miniclass ドライバーの[**チェンジャー Miniclass ドライバールーチンの Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/storage/driverentry-of-changer-miniclass-drivers)の使用方法が異なります。

    Windows 2000 では、チェンジャークラスドライバーの**Driverentry**ルーチンは、i/o 要求のエントリポイントの初期化など、さまざまなドライバー初期化タスクを実行します。 Windows XP 以降のオペレーティングシステムでは、miniclass ドライバーの**Driverentry**ルーチンで初期化が行われます。 Miniclass ドライバーの**Driverentry**ルーチンで実行する必要があるタスクの詳細については、「[必要なチェンジャー Miniclass ルーチン](required-changer-miniclass-routines.md)」を参照してください。

2.  *Classpnp*ライブラリルーチンにアクセスするさまざまな手段。

    ディスク、テープ、CD-ROM、およびチェンジャーデバイスのクラスドライバーは、 *classpnp*ライブラリを使用します。これは、オペレーティングシステム固有のデバイスに依存しないルーチンのコレクションを格納するシステム提供の DLL です。

    システム提供のほとんどのストレージクラスドライバーは、 *classpnp*ライブラリにあるルーチンと同様の一連の主要ルーチンを提供します。 これは、miniclass ドライバーが classpnp を直接呼び出すのではなく、クラスドライバールーチンを呼び出すことができるようにするためです *。* これにより、miniclass ドライバーが*classpnp* DDI に変更されるのを防ぐことができます。

    Windows 2000 チェンジャー miniclass ドライバーは、このルールの例外です。 Windows 2000 では、チェンジャークラスドライバーは miniclass ドライバーに*classpnp*ルーチンを間接的に呼び出す機能を提供しません。 このため、Windows 2000 では、チェンジャー miniclass ドライバーは*classpnp*ルーチンを直接呼び出すか、同等のルーチンを行で呼び出す必要があります。 *Classpnp*ルーチンを直接呼び出す Miniclass ドライバーは、 *classpnp*ライブラリに対して、ドライバーのサイズを大軍て静的にリンクする必要があります。 ドライバーが*classpnp*と動的にリンクする場合、以降のリリースでこのライブラリを変更すると、ドライバーが誤動作する可能性があります。

    Windows XP 以降のオペレーティングシステムでは、 *classpnp*ライブラリの直接呼び出しによって提供されていた最も重要なサービスのいくつかが、チェンジャークラスのドライバーによって提供されています。 そのため、Windows XP 以降のオペレーティングシステムでは、通常、チェンジャー miniclass ドライバーが*classpnp*を直接呼び出す必要はありません。

3.  Windows XP チェンジャークラスのドライバーには、Windows 2000 では使用できないルーチンが用意されています。 次の説明では、この違いについて説明します。

Windows 2000 では、チェンジャークラスドライバーは、miniclass ドライバーがを呼び出すために次のルーチンを提供します。

-   [**Changerclassallocatepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changerclassallocatepool) --プールメモリを割り当てます。

-   [**Changerclassfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changerclassfreepool) --プールメモリを解放します。

-   [**Changerclassdebugprint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changerclassdebugprint) --デバッグ情報を出力します。

Windows XP 以降のオペレーティングシステムでは、チェンジャークラスのドライバーは、前に示したルーチンに加えて、2つの追加ルーチンを提供します。

-   [**Changerclassinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changerclassinitialize) --チェンジャー miniclass ドライバーは、ドライバーを初期化するために、 **driverentry**ルーチン内から**changerclassinitialize**を呼び出します。 **Changerclassinitialize**は、以前は Windows 2000 チェンジャークラスドライバーの**driverentry**ルーチンによって実行された多くのタスクを実行します。

-   [**Changerclasssendsrbsynchronous**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changerclasssendsrbsynchronous) --SRB を初期化し、指定されたターゲットデバイスに同期的に送信します。

 

 




