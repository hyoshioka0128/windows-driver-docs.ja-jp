---
title: GFlags
description: GFlags (グローバル フラグ エディター)、gflags.exe、有効および無効にします。 は、高度なデバッグ、診断、およびトラブルシューティング機能。
ms.assetid: e268af2e-90a9-411e-8e29-ab486d2aac48
keywords: GFlags、グローバル フラグのエディター gflags.exe
ms.date: 06/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: cfa08a777d1e4a9e5fd7c59687fb5a7f419aef18
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537769"
---
# <a name="gflags"></a>GFlags


GFlags (グローバル フラグ エディター)、gflags.exe、有効および無効にします。 は、高度なデバッグ、診断、およびトラブルシューティング機能。 その他のツールを追跡するインジケーター、数、およびログを有効にする最もよく使用されます。

## <a name="span-idwheretogetgflagsspanspan-idwheretogetgflagsspanspan-idwheretogetgflagsspanwhere-to-get-gflags"></a><span id="Where_to_get_GFlags"></span><span id="where_to_get_gflags"></span><span id="WHERE_TO_GET_GFLAGS"></span>GFlags の入手先


含まれている GFlags、[デバッグ ツールの Windows 10 (WinDbg)](debugger-download-tools.md)します。

デバッグ ツールがインストールされている 64 ビット Windows で使用するための gflags.exe が既定では、次のディレクトリにインストールされます。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64
```

Windows の 32 ビット バージョンを実行している場合は、ここにある gflags.exe の 32 ビット バージョンを使用します。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86
```


## <a name="span-idddkgflagsdtoolsspanspan-idddkgflagsdtoolsspanoverview-of-gflags"></a><span id="ddk_gflags_dtools"></span><span id="DDK_GFLAGS_DTOOLS"></span>GFlags の概要


ドライバー開発者およびテスト担当者は多くの場合、ログ記録、デバッグを有効にする GFlags を使用して、直接、またはテスト スクリプトに GFlags コマンドを含めることにより、機能をテストします。 ページ ヒープの検証機能は、メモリ リークおよびカーネル モード ドライバーのバッファーのエラーを特定するのに役立ちます。

GFlags には、ダイアログ ボックスとコマンド ライン インターフェイスの両方があります。 ほとんどの機能は、両方のインターフェイスから使用が 1 つのインターフェイスの一部の機能はアクセスできます。 (を参照してください[GFlags 詳細](gflags-details.md))。

### <a name="span-idnewfeaturesspanspan-idnewfeaturesspanfeatures"></a><span id="new_features"></span><span id="NEW_FEATURES"></span>機能

-   ヒープのページ検証します。 GFlags には pageheap によって (pageheap.exe) ヒープ割り当ての監視を有効にするツールの機能が含まれています。 Pageheap によっては、以前のバージョンの Windows に含まれていました。

-   特別なプールの機能に必要な再起動は不要です。 Windows Vista および Windows の以降のバージョンでは、有効にする、無効にする、およびできます (「再起動」) を再起動しなくても、特別なプール機能を構成するコンピューター。 詳しくは、[特別なプール](special-pool.md)を参照してください。

-   オブジェクトの参照を追跡します。 新しいフラグは、オブジェクトを参照して、カーネル オブジェクトが逆参照のトレースを有効します。 Windows のこの新機能では、オブジェクトの参照カウントがデクリメントされた回数が多すぎますかにもかかわらずオブジェクトにないデクリメントは使用されなくときを検出します。 このフラグは、Windows Vista および Windows の以降のバージョンでのみサポートされます。

-   新しいダイアログ ボックスのデザイン。 GFlags ダイアログ ボックスがタブ付きのページを簡単に移動。

### <a name="span-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="requirements"></span><span id="REQUIREMENTS"></span>要件

レジストリまたはカーネル モードの場合、またはページ ヒープ検証を有効にすると、フラグを設定するなど、ほとんどの GFlags 機能を使用するには、コンピューターの Administrators グループのメンバーがあります。 Windows Vista では、ユーザーにする前に、最小のゲスト アカウントのアクセスがからプログラムを起動、**グローバル フラグ** ダイアログ ボックス。

機能するには、またはしないで動作は異なり、特定のオペレーティング システムのバージョンでは、ときに違いは、機能の説明について説明します。

このトピックには次が含まれます。

[GFlags の概要](gflags-overview.md)

[GFlags の詳細](gflags-details.md)

[**GFlags コマンド**](gflags-commands.md)

[GFlags フラグ テーブル](gflags-flag-table.md)

[GFlags と pageheap によって](gflags-and-pageheap.md)

[グローバル フラグ ダイアログ ボックス](global-flags-dialog-box.md)

[GFlags 例](gflags-examples.md)

[グローバル フラグの参照](global-flag-reference.md)

**注**  このツールの不適切な使用がシステム パフォーマンスが低下または起動を妨げる Windows、Windows を再インストールする必要はありません。

 

**重要な**  完全に Windows Server 2003 と以降のバージョンの Windows Vista を含む、Windows で有効でプールのタグ付けします。 これらのシステムで、**プール タグ付けを有効にする**チェック ボックスをオン、**グローバル フラグ** ダイアログ ボックスが淡色表示され、有効または無効にするためのコマンドは、タグ付けの失敗をプールします。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Windows 用デバッグ ツールに含まれるツール](extra-tools.md)

 

 






