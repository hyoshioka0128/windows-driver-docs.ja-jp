---
title: GFlags と pageheap によって
description: GFlags と pageheap によって
ms.assetid: 9ced92d9-b37c-4db5-b3f9-fa2fe5325e57
keywords:
- GFlags、GFlags および pageheap によって
- Pageheap によって (pageheap.exe)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd97a2fdb94d1d9343ed3122655ff52d0bd7c4fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529905"
---
# <a name="gflags-and-pageheap"></a>GFlags と pageheap によって


## <span id="ddk_gflags_and_pageheap_dtools"></span><span id="DDK_GFLAGS_AND_PAGEHEAP_DTOOLS"></span>


このバージョン GFlags には pageheap によって (pageheap.exe)、Windows での監視のヒープ割り当てができるようにするツールの機能が含まれます。 Pageheap によっては、メモリ割り当てを超えたへのアクセスの試みを検出するには、各割り当ての境界にメモリを予約する Windows 機能を有効します。

GFlags let でページ ヒープのオプションを選択する*標準ヒープ検証*、塗りつぶしが各ヒープの割り当ての最後にパターンし、パターンを調べ、割り当てが解放されると、書き込むまたは*完全ページ ヒープ検証*割り当てを超えるメモリにアクセスした場合、プログラムがすぐに停止できるように各割り当ての最後にアクセスできないページを挿入します。 完全なヒープの検証は、各割り当ての完全なメモリのページを使用するための広範囲にわたる使用可能性がシステム メモリ不足。

-   すべてのプロセスの標準的なページ ヒープの検証を有効にするには、 **gflags/r + hpa**または**gflags/k + hpa**します。

-   1 つのプロセスの標準的なページ ヒープの検証を有効にするには、 **gflags/p/enable** *ImageFileName*します。

-   1 つのプロセスの完全ページ ヒープの検証を有効にするには、 **gflags/i** *ImageFileName* **+ hpa**または**gflags/p/enable** *ImageFileName* **フル/** します。

除くすべてのページ ヒープの設定、 **/k**はレジストリに格納され、それらを変更するまでの有効なままです。

解釈するときに注意を払って、**ページ ヒープを有効にする**GFlags ダイアログ ボックスで、イメージ ファイルのチェック ボックス。 いっぱいになっているかどうか、または標準的なページ ヒープの検証は示しませんが、イメージ ファイルをヒープのページ検証が有効になっていることを示します。 チェックの結果から、チェック ボックスを選択し、完全な場合は、イメージ ファイルのページ ヒープの検証が有効にします。 ただし場合は、コマンド ライン インターフェイスを使用して、チェックの結果、チェックを表現できますイメージ ファイルのいずれかまたは標準ページ ヒープの検証を有効にします。

プログラムは、コマンドラインで、ヒープの完全なまたは標準のページ検証が有効になっているかどうかを判断するには、入力**gflags/p**します。 結果の表示で**トレース**プログラムの標準的なページ ヒープの検証が有効であることを示しますと**完全なトレース**プログラムの完全ページ ヒープの検証が有効であることを示します。

 

 





