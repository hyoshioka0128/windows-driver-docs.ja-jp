---
title: 例 11 有効にするとページ ヒープの検証
description: 例 11 有効にするとページ ヒープの検証
ms.assetid: 5d0303a9-29f7-4759-ae7b-ad670eaee0ee
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: fbcf00019ca2620cb3883d868e90a72830207bef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347820"
---
# <a name="example-11-enabling-page-heap-verification"></a>例 11:ページ ヒープ検証を有効にする


## <span id="ddk_example_11___enabling_page_heap_verification_dtools"></span><span id="DDK_EXAMPLE_11___ENABLING_PAGE_HEAP_VERIFICATION_DTOOLS"></span>


次のコマンドは、myapp.exe、架空のプログラムの完全および標準的なページ ヒープの検証を有効にします。

最初のコマンドは、有効*標準*myapp.exe のヒープの検証 ページします。 使用して、 **/p**プロセス ページ ヒープを有効にするパラメーター。 既定では、 **/p**標準ページ ヒープを使用します。

```console
gflags /p /enable myapp.exe 
```

次のコマンドを有効にする*完全*myapp.exe プログラムのヒープの検証 ページします。 これらのコマンドは、レジストリのさまざまな設定を作成するにはすべてを選択すると同等の機能、**ページ ヒープを有効にする**の myapp.exe のイメージ ファイルのチェック ボックス、**グローバル フラグ**ダイアログ ボックス。 これらのメソッドは、同じ意味で使用できます。

```console
gflags /p /enable myapp.exe /full
gflags /i myapp.exe +hpa
gflags /i myapp.exe +02000000
```

次のコマンドは、ページ ヒープの検証を有効にするために使用するコマンドやダイアログ ボックス メソッドにかかわらず、myapp.exe プログラムの完全なまたは標準ページ ヒープの検証を無効にします。

```console
gflags /p /disable myapp.exe
gflags /i myapp.exe -hpa
gflags /i myapp.exe -02000000
```

**注**  を使用する場合、 **/debug**または **/kdebug**パラメーターを使用して、 **/p/disable**パラメーター ページをオフにヒープの検証 (not **/i hpa**パラメーター)。 **/P/disable**パラメーター ページ ヒープの検証を無効にして、デバッガーを読み取るレジストリ エントリを削除します。

 

 

 





