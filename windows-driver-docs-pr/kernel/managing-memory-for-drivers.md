---
title: Windows ドライバーのメモリ管理
description: カーネルモードドライバーは、内部データの格納、i/o 操作中のデータのバッファリング、他のカーネルモードおよびユーザーモードコンポーネントとのメモリの共有などの目的にメモリを割り当てます。
ms.assetid: e030a37c-26ab-4177-9980-4336928975e1
keywords:
- メモリ管理 (WDK カーネル)
- 使用可能な領域 WDK カーネル
- 空き領域 WDK カーネル
- 領域 WDK 「メモリ WDK」を参照
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8ba2e0c5e31b9cc0dd739792343ff2caa810238
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827876"
---
# <a name="memory-management-for-windows-drivers"></a>Windows ドライバーのメモリ管理


カーネルモードドライバーは、内部データの格納、i/o 操作中のデータのバッファリング、他のカーネルモードおよびユーザーモードコンポーネントとのメモリの共有などの目的にメモリを割り当てます。 ドライバー開発者は、割り当てられたメモリを正確かつ効率的に使用するために、Windows のメモリ管理を理解している必要があります。 Windows は仮想メモリと物理メモリを管理し、メモリを別のユーザーとシステムのアドレス空間に分割します。 ドライバーは、割り当てられたメモリが、要求のページング、データのキャッシュ、命令の実行などの機能をサポートするかどうかを指定できます。




*メモリマネージャー*は、Windows のメモリ管理操作を実行するカーネルコンポーネントです。 詳細については、「 [Windows カーネルモードのメモリマネージャー](windows-kernel-mode-memory-manager.md)」を参照してください。

メモリマネージャーでは、ドライバーがメモリの割り当てと管理を行うために呼び出すカーネルモードサポートルーチンが多数実装されています。 詳細については、「[メモリ割り当てとバッファー管理](https://docs.microsoft.com/windows-hardware/drivers/ddi/_kernel/#memory-allocation-and-buffer-management)」を参照してください。

カーネルモードドライバーのメモリ管理機能は、ユーザーモードアプリケーションとは異なります。 アプリケーションのメモリ管理の詳細については、「[メモリ管理](https://docs.microsoft.com/windows/desktop/Memory/memory-management)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容


-   [Windows のメモリ領域の概要](overview-of-windows-memory-space.md)
-   [システム領域メモリの割り当て](allocating-system-space-memory.md)
-   [レジスタのマップ](map-registers.md)
-   [バスの相対アドレスを仮想アドレスにマップする](mapping-bus-relative-addresses-to-virtual-addresses.md)
-   [カーネルスタックの使用](using-the-kernel-stack.md)
-   [ルックアサイドリストの使用](using-lookaside-lists.md)
-   [ドライバーのページングの作成](making-drivers-pageable.md)
-   [読み取り専用システムメモリへのアクセス](accessing-read-only-system-memory.md)
-   [ユーザー領域のメモリへのアクセス](accessing-user-space-memory.md)
-   [実行なし (NX) の非ページプール](no-execute-nonpaged-pool.md)
-   [セクションのオブジェクトとビュー](section-objects-and-views.md)
-   [MDLs の使用](using-mdls.md)

 

 




