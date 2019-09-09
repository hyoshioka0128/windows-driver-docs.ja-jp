---
title: P (Windows デバッガー用語集)
description: 用語集のページ-P
ms.assetid: 4cfad26c-d8c0-4f80-aa54-b9cadbc84df3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcde64d30d167868f498fa484cb509dae5c70999
ms.sourcegitcommit: 48c4b6d3a504583d2f588ed892a4a281d4b58301
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70387027"
---
# <a name="p"></a>P


<span id="page_table"></span><span id="PAGE_TABLE"></span>**ページテーブル**  
仮想メモリアドレスを物理メモリアドレスにマップするプロセス固有のテーブル。

<span id="page_table_entry__pte_"></span><span id="PAGE_TABLE_ENTRY__PTE_"></span>**ページテーブルエントリ (PTE)**  
ページテーブル内の項目。

<span id="paged_pool"></span><span id="PAGED_POOL"></span>**ページプール**  
ディスクにページングできるシステムメモリの一部。

この用語は、実際にディスクにページアウトされたメモリを参照するだけではなく、オペレーティングシステムに許可されているメモリも含まれていることに注意してください。

<span id="paging"></span><span id="PAGING"></span>**ベル**  
物理メモリがいっぱいになったときにメモリマネージャーがページをメモリからディスクに転送する仮想メモリ操作。 *ページフォールト*は、メモリ内にないページにスレッドがアクセスしたときに発生します。

<span id="parent_symbol"></span><span id="PARENT_SYMBOL"></span>**親シンボル**  
他のシンボルに含まれる*記号*。たとえば、構造体にはそのメンバーが含まれます。

「*子シンボル*」も参照してください。

詳細については、「[スコープとシンボルグループ](scopes-and-symbol-groups.md)」を参照してください。

<span id="primary_client"></span><span id="PRIMARY_CLIENT"></span>**プライマリクライアント**  
現在のデバッグセッションに参加しているクライアントオブジェクト

詳細については、「[クライアントオブジェクト](client-objects.md)」を参照してください。

<span id="process_server"></span><span id="PROCESS_SERVER"></span>**プロセスサーバー**  
プロキシとして機能するデバッガーエンジンのインスタンス。スマートクライアントからの接続をリッスンし、これらのリモートクライアントによって要求されたメモリ、プロセッサ、または Windows の操作を実行します。

「*デバッグサーバー*」も参照してください。

詳細については、「[プロセスサーバー (ユーザーモード)](process-servers--user-mode-.md) 」および「プロセスサーバーとスマートクライアント」を参照してください。

<span id="processor_breakpoint"></span><span id="PROCESSOR_BREAKPOINT"></span>**プロセッサのブレークポイント**  
プロセッサによって実装されるブレークポイント。 デバッガーエンジンは、このブレークポイントを挿入するようにターゲットのプロセッサに指示します。

「ソフトウェアブレークポイント」も参照してください。 「*ソフトウェアブレークポイント*」も参照してください。

詳細については、「[ブレークポイントの使用](using-breakpoints.md)」を参照してください。

 

 





