---
title: 例 4 の複数のフラグの設定
description: 例 4 の複数のフラグの設定
ms.assetid: b8c7301b-4a34-4f03-8c5e-ba43a1fb3681
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: e11c0db223385480076b1aea7d84458541516dc4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539409"
---
# <a name="example-4-setting-multiple-flags"></a>例 4:複数のフラグの設定


## <span id="ddk_example_4___setting_multiple_flags_dtools"></span><span id="DDK_EXAMPLE_4___SETTING_MULTIPLE_FLAGS_DTOOLS"></span>


次のコマンドでは、現在のセッションに対してこれら 3 つのフラグを設定します。

-   [ヒープの無料のチェックを有効に](enable-heap-free-checking.md)(hfc、0x20)

-   [ヒープ パラメーター チェックを有効に](enable-heap-parameter-checking.md)(hpc、0x40)

-   [呼び出しでヒープの検証を有効にする](enable-heap-validation-on-call.md)(hvc、0x80)

このコマンドを使用して、 **/k**パラメーターをカーネル モード (セッションのみ) を指定します。 カーネル モードの値を設定**E0** (0xE0)、選択したフラグ (0x20 + 0x40 + 0x80) の 16 進数の値の合計。

```console
gflags /k e0 
```

応答、GFlags フラグがセッションの設定の変更後の値が表示されます。 表示では、コマンドが成功したことと、コマンドで指定された 3 つのフラグが設定されていることを示します。

```console
Current Running Kernel Settings are: 000000e0
    hfc - Enable heap free checking
    hpc - Enable heap parameter checking
    hvc - Enable heap validation on call
```

フラグを設定するのには、いくつかの異なる GFlags コマンドを使用できます。 この例で使用されるコマンドと同じ効果がそれぞれ次のコマンドとメソッドを同じ意味で使用することができます。

```console
gflags /k +20 +40 +80 
gflags /k +E0 
gflags /k +hfc +hpc +hvc 
```

(実行時) カーネル フラグがすぐに有効と、Windows のシャット ダウンするまでの有効なままです。

 

 





