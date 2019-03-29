---
title: チェンジャー クラス ドライバーのバージョンの違い
description: チェンジャー クラス ドライバーのバージョンの違い
ms.assetid: 4ae4d1b0-cf2f-4c81-b8ae-3a91fd479a89
keywords:
- チェンジャー ドライバー WDK ストレージ クラス ドライバー
- 記憶域チェンジャー ドライバー WDK、クラス ドライバー
- チェンジャー ドライバーのクラス ドライバー WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c68c604a9722e02287c75425b9d6d9a37974a5f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578450"
---
# <a name="differences-in-changer-class-driver-versions"></a>チェンジャー クラス ドライバーのバージョンの違い


## <span id="ddk_differences_in_changer_class_driver_versions_kg"></span><span id="DDK_DIFFERENCES_IN_CHANGER_CLASS_DRIVER_VERSIONS_KG"></span>


Windows XP および Windows 2000 チェンジャー クラス/miniclass ドライバー pair の実装の 3 つの主な違いがあります。

1.  別の使用、 [**チェンジャー Miniclass ドライバーの DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff552647) miniclass ドライバーで日常的な。

    Windows 2000 の場合、チェンジャー クラス ドライバーの**DriverEntry**ルーチンが I/O 要求のエントリ ポイントの初期化を含め、さまざまなドライバーの初期化タスクを実行します。 Windows XP およびそれ以降のオペレーティング システムでは、初期化が行われ、 **DriverEntry** miniclass ドライバーの日常的な。 参照してください[必要チェンジャー Miniclass ルーチン](required-changer-miniclass-routines.md)タスクの詳細についてを miniclass ドライバーの**DriverEntry**を実行するルーチンが必要です。

2.  別の手段へのアクセスの*classpnp.sys*ライブラリ ルーチン。

    ディスク、テープ、CD-ROM、およびチェンジャーのデバイス用のクラス ドライバーの使用、 *classpnp.sys*ライブラリ、特定のオペレーティング システム、デバイス非依存のルーチンのコレクションを格納するシステム提供の DLL。

    ほとんどのシステムが指定したストレージ クラス ドライバーについては、ルーチンのようなキーのルーチンのセットを提供する、 *classpnp.sys*ライブラリ。 これは、その miniclass ドライバーへの直接呼び出しではなく、クラス ドライバーのルーチンを呼び出すことができますのでする*classpnp.sys します。* これにより、保護 miniclass ドライバーへの変更を*classpnp.sys* DDI します。

    Windows 2000 でチェンジャー クラス ドライバーが提供しないため miniclass ドライバー機能を呼び出すのため、Windows 2000 チェンジャー miniclass ドライバーは、この規則の例外、 *classpnp.sys*ルーチン間接的にします。 したがって、Windows 2000 でチェンジャー miniclass ドライバーする必要がありますいずれかの呼び出し、 *classpnp.sys*ルーチンに直接または行で同等のルーチンを呼び出し。 呼び出す miniclass ドライバー *classpnp.sys*直接ルーチンにリンクする必要があります、 *classpnp.sys*ライブラリ、ドライバーのサイズを静的に swelling します。 ドライバーが動的にリンクする場合*classpnp.sys*、今後のリリースでは、このライブラリへの変更が原因で、ドライバーが正しく機能しません。

    Windows XP およびそれ以降のオペレーティング システムでは、いくつかの最も重要なサービスが提供していたへの直接呼び出し、 *classpnp.sys*チェンジャー クラス ドライバーによってライブラリが提供されます。 そのため、Windows XP およびそれ以降のオペレーティング システムでは、必要はありませんは、通常を呼び出すチェンジャー miniclass ドライバー *classpnp.sys*ライブラリ ルーチンに直接します。

3.  Windows XP チェンジャー クラス ドライバーは、Windows 2000 では使用できないルーチンを提供します。 以降の説明では、この違いを調べます。

Windows 2000 でチェンジャー クラス ドライバーは、次のルーチンを呼び出す miniclass ドライバーを提供します。

-   [**ChangerClassAllocatePool** ](https://msdn.microsoft.com/library/windows/hardware/ff551402) -プールのメモリを割り当てます。

-   [**ChangerClassFreePool** ](https://msdn.microsoft.com/library/windows/hardware/ff551411) -プールのメモリを解放します。

-   [**ChangerClassDebugPrint** ](https://msdn.microsoft.com/library/windows/hardware/ff551406) --デバッグ情報を出力します。

Windows XP およびそれ以降のオペレーティング システムでは、チェンジャー クラス ドライバーが提供するルーチンに加え、2 つの追加ルーチン以前表示されます。

-   [**ChangerClassInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff551413) --チェンジャー miniclass ドライバー呼び出し**ChangerClassInitialize**内からその**DriverEntry**ルーチン ドライバーを初期化します。 **ChangerClassInitialize** Windows 2000 チェンジャー クラス ドライバーで実行していた多くのタスクを実行します**DriverEntry**ルーチン。

-   [**ChangerClassSendSrbSynchronous** ](https://msdn.microsoft.com/library/windows/hardware/ff551415) --を初期化し、指定されたターゲット デバイスへ、SRB を同期的に送信します。

 

 




