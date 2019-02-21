---
title: グローバル フラグ ダイアログ ボックス
description: グローバル フラグ ダイアログ ボックス
ms.assetid: c6987d72-4141-45f2-af06-f4c7040a7e6b
keywords:
- GFlags、ダイアログ ボックス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3d514d8ac487435b4202eb8753b0e6caa3a167c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529585"
---
# <a name="global-flags-dialog-box"></a>グローバル フラグ ダイアログ ボックス


## <span id="ddk_global_flags_dialog_box_dtools"></span><span id="DDK_GLOBAL_FLAGS_DIALOG_BOX_DTOOLS"></span>


使用することができます、**グローバル フラグ** ダイアログ ボックスを設定し、名前ですべてのフラグを一覧表示するユーザー インターフェイスからのグローバル フラグをクリアします。 フラグの省略形または 16 進数の値を検索する必要はありません。

また、ダイアログ ボックスは、コマンドラインからは入手できず、次の機能へのアクセスを提供します。

-   **デバッガー** − では、特定のプログラムがデバッガーで常に実行を指定します。

-   **起動**− が指定したデバッグ設定でプログラムを実行します。

-   **カーネルの特別なプール タグ**− 特別なプール機能を構成します。

このトピックには、次の手順の指示が含まれます。

[ダイアログ ボックスを開く](opening-the-dialog-box.md)

[設定して、システム全体のフラグをクリアします。](setting-and-clearing-system-wide-flags.md)

[設定して、カーネル フラグをクリアします。](setting-and-clearing-kernel-flags.md)

[設定して、イメージ ファイルのフラグをクリアします。](setting-and-clearing-image-file-flags.md)

[フラグを使用してプログラムを起動します。](launching-a-program-with-flags.md)

[デバッガーでプログラムを実行します。](running-a-program-in-a-debugger.md)

[特別なプールを構成します。](configuring-special-pool.md)

[オブジェクト参照のトレースの構成](configuring-object-reference-tracing.md)

プールのタグ付けは無期限に Windows Server 2003 および以降のバージョンの Windows で有効にします。 これらのシステムで、**プール タグ付けを有効にする**チェック ボックスをオン、**グローバル フラグ** ダイアログ ボックスは淡色表示になり、プール タグ付けの失敗を有効または無効にするコマンド。

解釈するときに注意を払って、**ページ ヒープを有効にする**のイメージ ファイルのチェック ボックス、**グローバル フラグ** ダイアログ ボックス。 このチェック ボックスがいっぱいになっているかどうか、または標準的なページ ヒープの検証は示しませんが、イメージ ファイルをヒープのページ検証が有効になっていることを示します。 チェックの結果から、チェック ボックスを選択し、完全な場合は、イメージ ファイルのページ ヒープの検証が有効にします。 ただし場合は、コマンド ライン インターフェイスを使用して、チェックの結果、チェックを表現できますイメージ ファイルのいずれかまたは標準ページ ヒープの検証を有効にします。

プログラムは、コマンドラインで、完全なまたは標準ページ ヒープの検証が有効になっているかどうかを判断するには、入力**gflags/p**します。 結果の表示で**トレース**プログラムの標準的なページ ヒープの検証が有効であることを示しますと**完全なトレース**プログラムの完全ページ ヒープの検証が有効であることを示します。

 

 





