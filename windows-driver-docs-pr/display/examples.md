---
title: GpuMmu サンプル シナリオ
description: このトピックでは、一般的な使用シナリオとそれらを実装するために必要な操作手順について説明します。
ms.assetid: 30F7D158-3D99-40EE-8FED-48EC1615AC71
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51cf5e6417fdf4ad725cf2e06f9538f76d5e07ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527469"
---
# <a name="gpummu-example-scenarios"></a>GpuMmu サンプル シナリオ


このトピックでは、一般的な使用シナリオとそれらを実装するために必要な操作手順について説明します。

これらのシナリオは次のとおりです。

-   [プロセスのページ テーブル エントリを更新しています](#updating-page-table-entries-of-a-process)
-   [1 つの場所から別の割り当てのコンテンツを転送](#transferring-allocation-content-from-one-location-to-another)
-   [パターンを使用し、割り当てを入力](#filling-an-allocation-with-a-pattern)
-   [システム メモリに常駐している割り当てを行う](#making-an-allocation-resident-in-system-memory)
-   [メモリ マネージャーの制御構造体の初期化](#initialization-of-the-memory-manager-control-structures)

## プロセスのページ テーブル エントリを更新しています <a name="updating-page-table-entries-of-a-process"></a>


ここでは、物理メモリをプロセス (P) に属する割り当てをマップするページ テーブル エントリを更新する操作のシーケンスです。 ページ テーブルの割り当てが既にグラフィックス処理ユニット (GPU) のメモリ セグメントに常駐するいると見なされます。

1.  ビデオ メモリ マネージャがプロセス P. のルート ページ テーブルの割り当てのページングのプロセスのコンテキスト内の仮想アドレス範囲を割り当てる
2.  ビデオ メモリ マネージャがプロセス P. のページ テーブルの割り当てのページングのプロセスのコンテキスト内の仮想アドレス範囲を割り当てる
3.  ビデオ メモリ マネージャー呼び出し[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)で、 *UpdatePageTable*プロセス P ページにページング プロセス ページ テーブル エントリにマップするコマンドテーブルとページのディレクトリ。
4.  ビデオ メモリ マネージャー呼び出し[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)で、 *FlushTLB(PagingProcessRootPageTable)* コマンド。
5.  ビデオ メモリ マネージャー呼び出し[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)で、 *UpdatePageTable*物理アドレスを持つプロセスのページ テーブル エントリを入力するコマンド情報。
6.  ビデオ メモリ マネージャー呼び出し[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)で、 *FlushTLB (プロセス P ルート ページ テーブル)* コマンド。
7.  ページング プロセスのコンテキストで実行されるページング バッファーが送信されます。

![プロセスのページ テーブル エントリを更新しています](images/examples.1.png)

## 1 つの場所から別の割り当てのコンテンツを転送<a name="transferring-allocation-content-from-one-location-to-another"></a>


1 つの場所から別の (例: が割り当てのコンテンツを転送するときに、一連の操作を示します。 ローカル メモリからシステム メモリに)。

1.  ビデオ メモリ マネージャーは、ソースの割り当てとページング プロセス仮想アドレスのスクラッチ領域に変換先の割り当ての仮想アドレスの範囲を割り当てます。
2.  ビデオ メモリ マネージャー呼び出し[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)で、 *UpdatePageTable*コマンド。 コマンドは、ソース仮想アドレスの範囲のページングのプロセス ページ テーブル エントリをローカルの GPU メモリの割り当ての物理アドレスにマップします。
3.  ビデオ メモリ マネージャー呼び出し[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)で*UpdatePageTable*コマンド。 コマンドは、変換先の仮想アドレスのページングのプロセス ページ テーブル エントリをシステム メモリにマップします。
4.  ビデオ メモリ マネージャー呼び出し[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)で、 *FlushTLB (ページング プロセス ルート ページ テーブル)* します。
5.  ビデオ メモリ マネージャー呼び出し[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)で、 *TransferVirtual*転送操作を実行するコマンド。
6.  ページング バッファーは、ページング プロセスのコンテキストで実行するための GPU に送信されます。

![1 つの場所から別の割り当てのコンテンツを転送](images/examples.2.png)

## パターンを使用し、割り当てを入力 <a name="filling-an-allocation-with-a-pattern"></a>


割り当ては、パターンを格納する必要がある場合は、一連の操作にはここで。

1.  ビデオ メモリ マネージャーでは、ページング プロセス仮想アドレスのスクラッチ領域に変換先の割り当ての仮想アドレス範囲が割り当てられます。
2.  ビデオ メモリ マネージャー呼び出し[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)で、 *UpdatePageTable*コマンド。 コマンドは、変換先の仮想アドレスのページングのプロセス ページ テーブル エントリをマップします。
3.  ビデオ メモリ マネージャー呼び出し[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)で、 *FlushTLB (ページング プロセス ルート ページ テーブル)* します。
4.  ビデオ メモリ マネージャー呼び出し[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)で、 *FillVirtual*操作を実行するコマンド。
5.  ページング バッファーは、ページング プロセスのコンテキストで実行するための GPU に送信されます。

![パターンを使用し、割り当てを入力](images/examples.3.png)

## <a name="making-an-allocation-resident-in-system-memory"></a>システム メモリに常駐している割り当てを行う


次の操作が実行されるときに[ **D3DKMTMakeResident** ](https://msdn.microsoft.com/library/windows/hardware/dn906775)は、割り当てに常駐するために呼び出されます。 アプリケーション プロセス ページのテーブルがメモリに常駐するいると見なされます。

アプリケーション スレッド コンテキスト。

1.  割り当てし、(割り当てがシステム メモリに常駐している場合) は、仮想アドレスの割り当ての範囲の物理システム メモリのページをピン留めします。
2.  アプリケーションのデバイスの新しいページング フェンス ID を生成します。
3.  送信、 [ **MakeResident** ](https://msdn.microsoft.com/library/windows/hardware/dn906775)ビデオ メモリ マネージャーのコマンドには、スレッドが動作していた。
4.  アプリケーションに戻ります。

ビデオ メモリ マネージャーのワーカー スレッド コンテキスト。

1.  (上記の対応するセクションを参照してください) アプリケーションのプロセス ページ テーブル エントリを更新します。
2.  割り当てがローカル メモリ セグメントに常駐している場合は、ゼロ (上記の対応するセクションを参照してください) を使用し、割り当てを入力します。
3.  送信、 *SignalSynchronizationObject*ページング フェンス ID を持つスケジューラにコマンド

## <a name="initialization-of-the-memory-manager-control-structures"></a>メモリ マネージャーの制御構造体の初期化


<span id="The_paging_process_initialization"></span><span id="the_paging_process_initialization"></span><span id="THE_PAGING_PROCESS_INITIALIZATION"></span>ページングのプロセスの初期化  

グラフィックス デバイスに切り替えられたときに、Microsoft DirectX グラフィックスのカーネルにページングのプロセス仮想アドレス空間を初期化します、 *D0*電源の状態のデバイス

1.  ページング プロセスが作成された[ *DxgkDdiCreateProcess*](https://msdn.microsoft.com/library/windows/hardware/dn906337)します。
2.  システム デバイスが作成された[ *DxgkDdiCreateDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559615)します。 この時点で、カーネル モード ドライバーでは、ページングのプロセス アドレス空間内の仮想アドレス範囲を予約できます。
3.  ページングのプロセスでは、ページのテーブルの割り当てが作成されます。
4.  ページ テーブルの割り当ては、仮想のアドレス指定機能の構造で定義されているメモリのセグメントにコミットされます。
5.  [*UpdatePageTable* ](https://msdn.microsoft.com/library/windows/hardware/ff560815)ページ テーブルを初期化するために操作が呼び出されています。

<span id="A_client_process_initialization"></span><span id="a_client_process_initialization"></span><span id="A_CLIENT_PROCESS_INITIALIZATION"></span>クライアント プロセスの初期化  

新しいプロセスが作成されると、DirectX グラフィックスのカーネルには。

-   最初のページ テーブルの割り当てを作成します。
-   プロセスから最初の割り当てが常駐行われたときに、ページのテーブルの割り当てを初期化します。

 

 

