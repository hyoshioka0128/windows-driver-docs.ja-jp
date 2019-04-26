---
title: グローバル フラグの 1 つを表示する例
description: グローバル フラグの 1 つを表示する例
ms.assetid: c1a1eafd-d70a-43f9-af90-33ddc33758fe
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: a635b2bfa7f0cb6b7f627f207564263c1a4ed3da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347796"
---
# <a name="example-1-displaying-global-flags"></a>例 1:グローバル フラグを表示する


## <span id="ddk_example_1___displaying_global_flags_dtools"></span><span id="DDK_EXAMPLE_1___DISPLAYING_GLOBAL_FLAGS_DTOOLS"></span>


コマンドは、レジストリに設定されているシステム全体のフラグ、セッション (カーネル モード) に設定されているシステム フラグおよびイメージ ファイルに設定されたフラグに、この例の表示で説明します。

次の GFlags コマンドでは、レジストリに設定されているシステム全体のフラグの現在の値が表示されます。 使用して、 **/r**システム全体のレジストリ エントリを指定するパラメーター。

```console
gflags /r 
```

応答、GFlags は、すべてのフラグのセットの合計とフラグのセットの一覧を表す 1 つの 16 進値を表示します。

```console
Current Boot Registry Settings are: 40001400
    ptg - Enable pool tagging
    ust - Create user mode stack trace database
    bhd - Enable bad handles detection
```

この例では、結果は、0x40001400 の合計値と、3 つのタグが設定されますを示します。

-   [プールのタグ付けを有効にする](enable-pool-tagging.md)(ptg) 0x400 を =

-   [ユーザー モードのスタック トレースのデータベースの作成](create-user-mode-stack-trace-database.md)(ust) 0x1000 を =

-   [無効なハンドルの検出を有効にする](enable-bad-handles-detection.md)(bhd) 0x40000000 を =

次のコマンドは、現在のセッションに対して設定されているフラグを表示します。 使用して、 **/k**パラメーターをカーネル モードを示します。

```console
gflags /k 
```

次のコマンドでは、イメージ ファイルの notepad.exe のレジストリでフラグのセットが表示されます。 使用して、 **/i**パラメーターを示すファイル モードのイメージを作成し、イメージ ファイルを指定します。

```console
gflags /i notepad.exe 
```

表示されるフラグ値が現在、有効なフラグ値可能性がありますできないことに注意してください。 Windows を再起動するまで、システム全体のフラグに変更は有効ではありません。 プログラムを再起動するまで、イメージ ファイルのフラグ設定を変更は有効ではありません。

 

 





