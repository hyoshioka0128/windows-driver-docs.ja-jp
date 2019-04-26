---
title: 例 7 のイメージ ファイルのすべてのフラグのクリア
description: 例 7 のイメージ ファイルのすべてのフラグのクリア
ms.assetid: 832c79de-07ca-4212-b3b3-ace396986ebb
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 079f2b24110e1d0116a998d2af87c57d944e5173
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351190"
---
# <a name="example-7-clearing-all-flags-for-an-image-file"></a>例 7:イメージ ファイルのすべてのフラグをクリアする


## <span id="ddk_example_7___clearing_all_flags_for_an_image_file_dtools"></span><span id="DDK_EXAMPLE_7___CLEARING_ALL_FLAGS_FOR_AN_IMAGE_FILE_DTOOLS"></span>


次のコマンドは、すべてのフラグとイメージ ファイルをイメージのデバッガー オプションをクリアします。 コマンドでは、フラグの現在の値に高い値 (0 xffffffff) を追加します。 GFlags を削除することによって応答、 **GlobalFlag**レジストリ エントリのイメージ ファイルに、すべての格納値が削除されます。

このコマンドでは、システム全体にフラグを設定には影響しません**GlobalFlag**セッション (カーネル モード) のレジストリ エントリまたはフラグを設定します。

```console
gflags /i notepad.exe ffffffff 
```

応答として、GFlags にイメージ ファイルのフラグのセットがないことを示すメッセージが表示されます。

```console
No Registry Settings for notepad.exe executable 
```

 

 





