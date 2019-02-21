---
title: RDBSS ドライバーとライブラリ
description: RDBSS ドライバーとライブラリ
ms.assetid: fb2d1939-7af5-474c-8247-e5d48b4bbed6
keywords:
- ネットワーク リダイレクター WDK、RDBSS
- リダイレクター ドライバー WDK、RDBSS
- カーネル ネットワーク リダイレクター WDK、RDBSS
- RDBSS WDK ファイル システム
- ファイル システム ドライバー WDK、RDBSS
- WDK のスタティック ライブラリのファイル システム
- RDBSS WDK ファイル システム、RDBSS について
- RDBSS についてのリダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム
- ミニ-リダイレクター WDK、RDBSS
- WDK RDBSS 構造体
- データ構造の WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49cda6750c52393893d524dc2ae72676de60bc33
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551989"
---
# <a name="the-rdbss-driver-and-library"></a>RDBSS ドライバーとライブラリ


## <span id="ddk_the_rdbss_driver_and_library_if"></span><span id="DDK_THE_RDBSS_DRIVER_AND_LIBRARY_IF"></span>


2 つの形式で、リダイレクトされたドライブのバッファリング サブシステム (RDBSS) に実装されます。

-   ファイル システム ドライバー (*rdbss.sys*) オペレーティング システムに付属します。

-   スタティック ライブラリ (*rdbsslib.lib*) と Windows Driver Kit (WDK) を指定します。

*Rdbss.sys*任意の非モノリシック ネットワーク ミニ-リダイレクターがシステムに登録されている場合、ドライバーが自動的に読み込まれます。 サーバー メッセージ ブロック (SMB) リダイレクター (*mrxsmb sys*) は現在非モノリシック ネットワーク ミニ リダイレクター ドライバーとしてビルドできる唯一のドライバーです。

その他のネットワーク ミニ リダイレクター ドライバーなどの他の Microsoft ネットワーク ミニ-リダイレクター、オペレーティング システムに付属しているとリンクするモノリシック ドライバーとして実装する必要があります、 *rdbsslib.lib*スタティック ライブラリWDK に付属します。

RDBSS は、ネットワーク ミニ リダイレクター ドライバー、I/O マネージャー、キャッシュ マネージャー、メモリ マネージャー、およびその他のカーネルのシステムとの通信を適切に定義されたメカニズムを使用します。

RDBSS は、多数のネットワークのミニ リダイレクターとオプションを設定し、さまざまな操作を実行するには、その他のカーネル システムで呼び出すことができるルーチンをエクスポートします。 RDBSS によってエクスポートされたルーチンを呼び出すには、ネットワーク ミニ リダイレクター ドライバー (またはその他のカーネル ドライバー) WDK の適切なヘッダー ファイルが含まれています、名前でエクスポートされた RDBSS ルーチンを呼び出すし、適切なリンク*rdbsslib.lib*ファイルWDK と共にインストールされます。 異なる*rdbsslib.lib*ファイルは、WDK Window Vista、Windows Server 2003、Windows XP、および Windows 2000 に付属します。

RDBSS の WDK のヘッダー ファイルもいくつかの RDBSS ルーチンの一部を直接呼び出すのではなく、ネットワークのミニ リダイレクター ドライバーによって使用するために推奨されているマクロを定義します。

すべての定義し、RDBSS で使用されるデータ構造により、検証で広く使用されているデータ構造体の先頭に特別な 4 バイト署名があります。 RDBSS データ構造体のこれらの署名の値は、WDK のヘッダー ファイルで定義されている*nodetype.h*します。 これらのデータ構造の署名は、トラブルシューティングとデバッグ RDBSS が使用され、ネットワーク ミニ リダイレクター ドライバー。

次のセクションでは、ルーチン RDBSS によってエクスポートされたもので、これらのルーチンの呼び出しに定義されているマクロのカテゴリの詳細ごとにについて説明します。 まず RDBSS および RDBSS によって定義されているマクロのようなリストによって提供されるルーチンのすべての一覧。

-   [RDBSS によって提供されるルーチン](routines-provided-by-rdbss.md)

-   [RDBSS によって定義されているマクロ](macros-defined-by-rdbss.md)

RDBSS とこれらのルーチンの呼び出しに定義されている RDBSS マクロによってエクスポートされたルーチンは、数、以下のさまざまなカテゴリに整理できます。

-   [ドライバーの登録と開始/停止の制御](driver-registration-and-start-stop-control.md)

-   [プールの割り当てと解放ルーチン](pool-allocation-and-free-routines.md)

-   [タイマーとワーカー スレッド管理](timer-and-worker-thread-management.md)

-   [作業のキュー メカニズムをディスパッチ](work-queue-dispatching-mechanisms.md)

-   [診断およびデバッグ](diagnostics-and-debugging.md)

-   [ログ記録ルーチンとマクロ](logging-routines-and-macros.md)

-   [その他のルーチン](miscellaneous-routines2.md)

-   [RX\_コンテキストと IRP の管理](rx-context-and-irp-management.md)

-   [接続およびファイル構造の管理](connection-and-file-structure-management.md)

-   [FCB とリソースの同期](fcb-resource-synchronization.md)

-   [バッファリング状態のコントロール](buffering-state-control.md)

-   [低い I/O ルーチン](low-i-o-routines.md)

-   [名前のキャッシュ管理](name-cache-management.md)

-   [プレフィックスのテーブルの管理](prefix-table-management.md)

-   [削除と清掃のコントロール](purging-and-scavenging-control.md)

-   [多重化 ID の管理](multiplex-id-management.md)

-   [エンジンの接続の管理](connection-engine-management.md)

 

 




