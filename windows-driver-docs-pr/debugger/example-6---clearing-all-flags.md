---
title: 例 6 のすべてのフラグをクリアします。
description: 例 6 のすべてのフラグをクリアします。
ms.assetid: 07a6af3d-3ef7-429d-9afa-439b20915ab1
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: d76940e358f53d82f4785332849140710e0316d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530069"
---
# <a name="example-6-clearing-all-flags"></a>例 6:すべてのフラグをクリアします。


## <span id="ddk_example_6___clearing_all_flags_dtools"></span><span id="DDK_EXAMPLE_6___CLEARING_ALL_FLAGS_DTOOLS"></span>


この例では、設定、レジストリとのセッションのすべてのフラグをクリアする 2 つの方法を示します。

-   現在のフラグ値を減算します。

-   高の値を減算します。

**注**  メソッドは、この例フラグをクリアのみで示されています。 既定値に最大スタックのトレースのサイズまたはカーネルの特別なプール タグをリセットするしません。

 

### <a name="span-idsubtractthecurrentflagvaluespanspan-idsubtractthecurrentflagvaluespanspan-idsubtractthecurrentflagvaluespansubtract-the-current-flag-value"></a><span id="Subtract_the_Current_Flag_Value"></span><span id="subtract_the_current_flag_value"></span><span id="SUBTRACT_THE_CURRENT_FLAG_VALUE"></span>現在のフラグ値を減算します。

次のコマンドは、エントリの現在の値を減算して、レジストリにシステム全体のフラグのエントリに設定するすべてのフラグをクリアします。 この例では、現在の値は 0xE0 です。 コマンドを使用して、 **/r**システム全体のレジストリ モードとマイナス記号 (-) E0 をフラグ値から減算する E0 値を示します。

```console
gflags /r -E0 
```

応答 GFlags はシステム全体のフラグのレジストリ エントリの変更後の値を表示します。 値 0 は、コマンドが成功したことと、レジストリに、システム全体のフラグ設定が不要になったことを示します。

```console
Current Boot Registry Settings are: 00000000 
```

次のコマンドが、この例で使用されるコマンドと同じ効果があるし、を置き換えて使用できることに注意してください。

```console
gflags /r -20 -40 -80 
gflags /r -hfc -hpc -hvc 
```

### <a name="span-idsubtracthighvaluesspanspan-idsubtracthighvaluesspanspan-idsubtracthighvaluesspansubtract-high-values"></a><span id="Subtract_High_Values"></span><span id="subtract_high_values"></span><span id="SUBTRACT_HIGH_VALUES"></span>減算の値が高い

次のコマンドは、システム全体のフラグ設定から値が大きい場合 (0 xffffffff) を差し引くことでシステム全体のすべてのフラグをクリアします。

```console
gflags /r -ffffffff 
```

応答 GFlags はシステム全体のフラグのエントリの変更後の値を表示します。 値 0 は、コマンドが成功したことと、レジストリに、システム全体のフラグ設定が不要になったことを示します。

```console
Current Boot Registry Settings are: 00000000 
```

**ヒント:**    、メモ帳にこのコマンドを入力し、clearflag.bat として保存します。 その後、すべてのフラグをクリアする入力**ClearFlag**します。

 

最後に、次の例では、すべてのフラグをオフにするとの直感的なメソッドが動作しないことを示します。

次のコマンドは、システム全体のフラグのエントリの値を 0 に設定が表示されます。 ただし、システム全体のフラグ値に 0 を実際に追加します。 この例では、システム全体のフラグのエントリの現在の値は 0xE0 です。

```console
gflags /r 0 
```

応答として、GFlags では、コマンドが完了した後にシステム全体のフラグの値が表示されます。

```console
Current Boot Registry Settings are: 000000e0
    hfc - Enable heap free checking
    hpc - Enable heap parameter checking
    hvc - Enable heap validation on call
```

コマンドはシステム全体のフラグのエントリに値 0 が追加されているためには影響しません。

 

 





