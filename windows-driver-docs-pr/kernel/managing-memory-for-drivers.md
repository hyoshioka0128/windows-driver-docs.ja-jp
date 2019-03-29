---
title: Windows ドライバーのメモリ管理
description: カーネル モード ドライバーでは、内部データを格納する、I/O 操作中にデータをバッファリングおよびその他のカーネル モードとユーザー モード コンポーネントとメモリの共有などの目的でメモリを割り当てます。
ms.assetid: e030a37c-26ab-4177-9980-4336928975e1
keywords:
- メモリ管理の WDK カーネル
- 使用可能な領域の WDK カーネル
- WDK カーネルの空き領域
- スペース メモリ WDK に WDK を参照してください。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 796ec13ccedf25e4c2ae2b48bd457087a9b3afc0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578283"
---
# <a name="memory-management-for-windows-drivers"></a>Windows ドライバーのメモリ管理


カーネル モード ドライバーでは、内部データを格納する、I/O 操作中にデータをバッファリングおよびその他のカーネル モードとユーザー モード コンポーネントとメモリの共有などの目的でメモリを割り当てます。 ドライバー開発者向けでは、Windows でのメモリ管理を使用するよう割り当てられたメモリ正常かつ効率的に理解する必要があります。 Windows では、仮想および物理メモリを管理し、メモリを別のユーザーとシステムのアドレス空間に分割します。 ドライバーは、割り当てられたメモリがデマンド ページング、データ キャッシュ、および命令の実行などの機能をサポートしているかどうかを指定できます。




*メモリ マネージャー*は Windows でのメモリ管理操作を実行するカーネル コンポーネントです。 詳細については、次を参照してください。 [Windows カーネル モードのメモリ マネージャー](windows-kernel-mode-memory-manager.md)します。

メモリ マネージャーは、さまざまなカーネル モードのサポート ルーチンの割り当てし、メモリを管理するドライバーを呼び出すことを実装します。 詳細については、次を参照してください。[メモリの割り当てとバッファー管理](https://msdn.microsoft.com/library/windows/hardware/ff554422)します。

カーネル モード ドライバーのメモリ管理機能がユーザー モード アプリケーションの異なるです。 アプリケーションのメモリ管理の詳細については、次を参照してください。[メモリ管理](https://msdn.microsoft.com/library/windows/desktop/aa366779)します。

## <a name="in-this-section"></a>このセクションの内容


-   [Windows メモリ領域の概要](overview-of-windows-memory-space.md)
-   [システム容量のメモリの割り当てください。](allocating-system-space-memory.md)
-   [レジスタをマップします。](map-registers.md)
-   [バスの相対アドレスを仮想アドレスにマップします。](mapping-bus-relative-addresses-to-virtual-addresses.md)
-   [カーネル スタックを使用してください。](using-the-kernel-stack.md)
-   [ルック アサイド リストの使用](using-lookaside-lists.md)
-   [ドライバーのページングを行う](making-drivers-pageable.md)
-   [読み取り専用のシステム メモリへのアクセス](accessing-read-only-system-memory.md)
-   [ユーザー領域のメモリにアクセスします。](accessing-user-space-memory.md)
-   [No-Execute (NX) 非ページ プール](no-execute-nonpaged-pool.md)
-   [セクション オブジェクトとビュー](section-objects-and-views.md)
-   [MDLs を使用します。](using-mdls.md)

 

 




