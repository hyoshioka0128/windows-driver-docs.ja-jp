---
title: シンボルの読み込みの遅延
description: シンボルの読み込みの遅延
ms.assetid: 58771089-dd0c-4ea9-8a9a-41553f290e88
keywords:
- シンボルの遅延読み込み
- シンボル、シンボルの読み込みの遅延
- シンボルの遅延読み込み
- シンボル、シンボルの読み込みの遅延
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 853eba6fce8395fb81e6a37e8e33bfefed0ba557
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553152"
---
# <a name="deferred-symbol-loading"></a>シンボルの読み込みの遅延


## <span id="ddk_deferred_symbol_loading_dbg"></span><span id="DDK_DEFERRED_SYMBOL_LOADING_DBG"></span>


既定では、シンボル情報が実際に読み込まれていない、ターゲット モジュールが読み込まれるときにします。 代わりに、必要とされるため、シンボルは、デバッガーによって読み込まれます。 これは呼び出されます*シンボルの読み込みの遅延*または*シンボルの遅延読み込み*します。 このオプションが有効になっているときに認識されていないシンボルを検出するたびにシンボルを読み込みます。

たとえばを使用して、シンボル パスが変更されたときに、 [ **.sympath (シンボル パスの設定)** ](-sympath--set-symbol-path-.md)エクスポート シンボルを使用したコマンド、読み込まれたすべてのモジュールが限定的に再読み込みします。 完全な PDB シンボルを使用したモジュールのシンボルは遅延を再読み込みする場合は、新しいパスが PDB シンボルの読み込みに使用された元のパスには含まれていません。 まだ、新しいパスには、PDB シンボル ファイルを元のパスが含まれているこれらのシンボルは遅れて読み込まれません。

遅延シンボルの読み込みを無効にすると、プロセスの起動が大幅に遅くなることができます、たびに、モジュールにすべてのシンボルを読み取るために読み込まれます。

シンボルを使用してモジュールのプレフィックスがない WinDbg、遅延のシンボルの読み込み動作を変更することができます、[修飾されていないシンボルの解決](debug---resolve-unqualified-symbols.md)オプションを**デバッグ**メニュー。

シンボルの遅延読み込みを使用してオーバーライドすることができます、 [ **%ld (シンボルの読み込み)** ](ld--load-symbols-.md)コマンドまたは[ **.reload (モジュールの再読み込み)** ](-reload--reload-module-.md)コマンド **/f**オプション。 これら強制的に他のシンボルの読み込みの遅延が指定したシンボルにすぐに読み込まれます。

既定では、シンボルの遅延読み込みが有効にします。 KD、CDB で、 **-s** [コマンド ライン オプション](command-line-options.md)このオプションをオフにします。 できますも無効にすることで CDB を使用して、 *LazyLoad*変数、 [tools.ini](configuring-tools-ini.md)ファイル。 デバッガーが実行されている場合、このオプションにできますオンまたはオフを使用して[ **.symopt + 0x4** ](-symopt--set-symbol-options-.md)または **.symopt 0x4**、それぞれします。

 

 





