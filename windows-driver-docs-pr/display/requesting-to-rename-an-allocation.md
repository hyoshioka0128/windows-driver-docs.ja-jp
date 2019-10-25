---
title: 割り当ての名前を変更する要求
description: 割り当ての名前を変更する要求
ms.assetid: f22e19ba-9ff3-4aa1-a3f0-103f67ea7c60
keywords:
- コマンドバッファー WDK 表示、割り当ての名前変更
- DMA バッファー WDK 表示、割り当ての名前変更
- WDK 表示の名前変更の割り当て
- 割り当ての名前の変更 (WDK 表示)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 844224d47849ed345441316cf5bbff49c250e630
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829585"
---
# <a name="requesting-to-rename-an-allocation"></a>割り当ての名前を変更する要求


ユーザーモードの表示ドライバーでは、アプリケーションがサーフェイスのコンテンツを (頂点バッファーなどの) ロック要求の一部として破棄することを指定した場合、ビデオメモリマネージャーがサーフェイスに関連付けられている割り当ての名前を変更するように要求する必要があります。 Microsoft Direct3D ランタイムは、**破棄**ビットフィールドフラグを渡して、サーフェイスの現在のコンテンツが不要になったことを示します。 ドライバーは、現在の割り当てがアイドル状態になるまでアプリケーションスレッドを停止するのではなく、画面の内容を保持している現在の割り当てがビジーである場合、ビデオメモリマネージャーがロック要求を処理するために新しい割り当てを割り当てるように要求できます。

ユーザーモードのディスプレイドライバーは、 [**D3DDDICB\_LOCKFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddicb_lockflags)構造体の**破棄**メンバーが[**pfnlockcb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb)関数の呼び出しで設定されている場合、ビデオメモリマネージャーが割り当ての名前を変更することを要求します。 ビデオメモリマネージャーは、割り当ての名前を変更する必要があるかどうかを判断します。割り当てが現在ビジー状態であり、現在のメモリ状態であるかどうかに基づいて、割り当てがアイドル状態になるまでアプリケーションを停止させます。 名前を変更する各割り当てについて、ビデオメモリマネージャーは、割り当てのロックに連続して使用される割り当ての一覧を保持します。 ビデオメモリマネージャーは、アプリケーションが割り当ての内容を破棄するたびに一覧を順番に表示します。 リストの長さは、アプリケーションの要件とメモリの負荷によって決まります。 ビデオメモリマネージャーは、ロック要求でのアプリケーションスレッドの停止を避けるために、リストを十分に保持しようとします。 ただし、メモリが不足している場合は、メモリ不足の原因を避けるために、ビデオメモリマネージャーが一覧をトリミングすることができます。

割り当ての名前変更リストの長さに制限を設けるために、ドライバーは、割り当てを作成するときに、 [**DXGK\_ALLOCATION info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)構造体の**MaximumRenamingListLength**メンバーを設定します。 ドライバーで**MaximumRenamingListLength**が0以外の値に設定されている場合、ビデオメモリマネージャーは、ドライバーによって課される制限を超えずに、名前変更リストの適切な長さを判断します。 ドライバーで**MaximumRenamingListLength**が0に設定されている場合、メモリマネージャーは、パフォーマンス向上のために必要なサイズになるように名前変更リストのサイズを大きくすることができます。

ユーザーモードの表示ドライバーで[**D3DDDICB\_LOCKFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddicb_lockflags)の**破棄**メンバーが設定されている場合、ビデオメモリマネージャーは、ディスプレイミニポートドライバーを呼び出して、元の割り当てに対する追加の割り当てを割り当てないことに注意してください。 ビデオメモリマネージャーは、元の割り当ての作成パラメーターを使用して、すべての追加割り当てを作成します。 ディスプレイミニポートドライバーの観点から見ると、同じ割り当てが複数の同時セグメントの場所でページングされています。

 

 





