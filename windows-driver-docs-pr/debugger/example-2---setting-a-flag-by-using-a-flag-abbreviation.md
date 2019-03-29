---
title: 例 2 のフラグの省略形を使用して、フラグの設定
description: 例 2 のフラグの省略形を使用して、フラグの設定
ms.assetid: 3c011ca5-8901-4bf2-b95d-364d644cb476
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: b4a3d2e7cff878921886a0b93bfa9ed6db721345
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571217"
---
# <a name="example-2-setting-a-flag-by-using-a-flag-abbreviation"></a>例 2:フラグの省略形を使用してフラグを設定する


## <span id="ddk_example_2___setting_a_flag_by_using_a_flag_abbreviation_dtools"></span><span id="DDK_EXAMPLE_2___SETTING_A_FLAG_BY_USING_A_FLAG_ABBREVIATION_DTOOLS"></span>


次のコマンド セット、[ローダーのスナップを表示する](show-loader-snaps.md)notepad.exe ファイルがイメージのフラグ。 **ローダーのスナップを表示する**は読み込みの詳細にキャプチャし、実行可能イメージとそのサポート ライブラリ モジュールのアンロード、読み込みプロセスのスナップショットを取得します。

コマンドを使用して、 **/i**パラメーターを示すファイル モードのイメージを作成し、イメージ ファイル notepad.exe の名前を指定します。 コマンドを使用して、フラグを識別するために**sls**の省略形**ローダーのスナップを表示する**、続きを示すフラグが設定されている正符号 (+) の省略形。 プラス記号をせず、コマンドには影響はありません。

```console
gflags /i notepad.exe +sls 
```

応答、GFlags は notepad.exe に設定されているフラグを表示します。 表示では、コマンドが成功したことを示します。 **ローダーのスナップを表示する**メモ帳プログラムのすべての新しいセッションの機能を有効にします。

```console
Current Registry Settings for notepad.exe executable are: 00000002
    sls - Show Loader Snaps
```

 

 





