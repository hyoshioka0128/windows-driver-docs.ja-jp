---
title: 例 5 フラグをクリアします。
description: 例 5 フラグをクリアします。
ms.assetid: 63c8bae9-ae6e-4d82-9389-ec36554635ab
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: d0de0975e41bc5452ececcc237f83a2cfa605398
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347730"
---
# <a name="example-5-clearing-a-flag"></a>例 5:フラグをクリアする


## <span id="ddk_example_5___clearing_a_flag_dtools"></span><span id="DDK_EXAMPLE_5___CLEARING_A_FLAG_DTOOLS"></span>


次のコマンドは、システム全体を消去します。[ページ ヒープを有効にする](enable-page-heap.md)フラグをレジストリに設定します。 コマンドを使用して、 **/r**をシステム全体のレジストリのモードを示すためにパラメーターと**hpa**の省略形、**ページ ヒープを有効にする**フラグ。 マイナス記号 (-) は、フラグがクリアすることを示します。

```console
gflags /r -hpa 
```

応答、GFlags、システム全体のレジストリ エントリの現在の値が表示されます。 表示は、コマンドが成功したことと、任意のフラグのセットが不要になったことを示します。

```console
Current Boot Registry Settings are: 00000000 
```

次のコマンドは、16 進数の値を使用して、**ページ ヒープを有効にする**フラグは、この例では、コマンドと同じ効果を使用します。 これらのコマンドは、同じ意味で使用できます。

```console
gflags /r -02000000 
```

 

 





