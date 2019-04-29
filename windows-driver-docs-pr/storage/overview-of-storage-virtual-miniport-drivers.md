---
title: 記憶域仮想ミニポート ドライバーの概要
description: 記憶域仮想ミニポート ドライバーの概要
ms.assetid: 5aee56e6-610c-4718-8566-9285682049cb
keywords:
- 記憶域仮想ミニポート ドライバー WDK, 概要
- 仮想ミニポート ドライバー WDK
- ミニポート ドライバー WDK ストレージ、仮想
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66912362b0e66c6938ab804e8e09d5bb8cc209d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389415"
---
# <a name="overview-of-storage-virtual-miniport-drivers"></a>記憶域仮想ミニポート ドライバーの概要


Windows vista Service Pack 1 (SP1) および Windows Server 2008、Storport インターフェイスの有用性を拡張するには、Microsoft が仮想ミニポート (VMiniport) ドライバー インターフェイスを定義します。 このインターフェイスは、物理ハードウェアの厳密なアソシエーションが現在ミニポート ドライバーに適していません。 これらの変更は、ハードウェアに関連付けられている (「物理」) のミニポート ドライバーのみ Storport ルーチンを呼び出すの制限を削除しないでください。 物理ミニポートのドライバーとは異なり、仮想のミニポート ドライバーは WDM ドキュメントの状態として Windows Driver Model (WDM) のルーチンへの呼び出しを実行できます。 特に明記しない限り、この時点から「ミニポート」という用語はされる「仮想ミニポート」を参照してください。

仮想ミニポート ドライバー インターフェイスは、メモリとの同期を処理するため、ポート ドライバー (Storport) に基づいて証明書利用者からミニポートを解放します。 インタ フェースでは、これまで使用できない方法で I/O を実行する仮想ミニポート ドライバーを使用します。 これらの変更は、対象に限定されませんが、将来の iSCSI や Infiniband 標準ストレージ インターフェイスなどの記憶域テクノロジを有効にします。

VMiniport ドライバーを実装する場合は、注意を使用します。 展開では、柔軟性を与える、ただし、パス、および I/O のタイミングを検証中に、エラーを検出するのには注意を要求します。 いくつかの例がここでは、提供されているがカーネル インターフェイスの使用可能なすべての結果を予測することはできません。

 

 




