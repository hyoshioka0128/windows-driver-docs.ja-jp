---
title: 例 3 の 16 進値を使用して、フラグの設定
description: 例 3 の 16 進値を使用して、フラグの設定
ms.assetid: 64fa0b2e-9fe7-47d0-bf83-8ae7c06252b6
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8ca853bd3c788025563a5ca358e9d1570605f225
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580141"
---
# <a name="example-3-setting-a-flag-by-using-its-hexadecimal-value"></a>例 3: 16 進値を使用してフラグを設定する


## <span id="ddk_example_3___setting_a_flag_by_using_its_hexadecimal_value_dtools"></span><span id="DDK_EXAMPLE_3___SETTING_A_FLAG_BY_USING_ITS_HEXADECIMAL_VALUE_DTOOLS"></span>


次のコマンドでは、システム全体の設定[ページ ヒープを有効にする](enable-page-heap.md)フラグ。 **ページ ヒープを有効にする**各ヒープの割り当てにガード ページとその他の追跡機能を追加します。

コマンドを使用して、 **/r**パラメーターをシステム全体のレジストリのモードを示します。 コマンドを使用して、フラグを識別するために**2000000**、0x2000000、16 進数の値を表す**ページ ヒープを有効にする**します。

プラス記号が省略されますが、コマンドは、フラグを設定、(+) 記号です。 符号がオプションであり、加算 (+) を 16 進数の値を使用する場合、既定値です。

```console
gflags /r 2000000 
```

応答、GFlags はレジストリに設定されているシステム全体のフラグを表示します。 表示では、コマンドが成功したことを示します。 **ページ ヒープを有効にする**Windows を再起動すると、すべてのプロセスの機能を有効になります。

```console
Current Boot Registry Settings are: 02000000
    hpa - Enable page heap
```

 

 





