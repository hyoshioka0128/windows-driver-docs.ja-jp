---
title: GpuMmu のサンプルシナリオ
description: このトピックでは、一般的な使用シナリオと、それらを実装するために必要な一連の操作について説明します。
ms.assetid: 30F7D158-3D99-40EE-8FED-48EC1615AC71
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 320e7cb653b1e51803c8a34e911b563508fe0b04
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839704"
---
# <a name="gpummu-example-scenarios"></a>GpuMmu のサンプルシナリオ


このトピックでは、一般的な使用シナリオと、それらを実装するために必要な一連の操作について説明します。

これらのシナリオは、次のとおりです。

-   [プロセスのページテーブルエントリを更新しています](#updating-page-table-entries-of-a-process)
-   [ある場所から別の場所への割り当てコンテンツの転送](#transferring-allocation-content-from-one-location-to-another)
-   [パターンを使用した割り当ての塗りつぶし](#filling-an-allocation-with-a-pattern)
-   [システムメモリに割り当てを常駐させる](#making-an-allocation-resident-in-system-memory)
-   [メモリマネージャーのコントロール構造体の初期化](#initialization-of-the-memory-manager-control-structures)

## プロセスのページテーブルエントリを更新しています<a name="updating-page-table-entries-of-a-process"></a>


プロセスに属する割り当て (P) を物理メモリにマップするために、ページテーブルエントリを更新する操作のシーケンスを次に示します。 ページテーブルの割り当ては、グラフィックス処理ユニット (GPU) のメモリセグメントに既に存在していることを前提としています。

1.  ビデオメモリマネージャーは、プロセス P のルートページテーブル割り当てのために、ページングプロセスコンテキストに仮想アドレス範囲を割り当てます。
2.  ビデオメモリマネージャーは、プロセス P のページテーブル割り当てのために、ページングプロセスコンテキストに仮想アドレス範囲を割り当てます。
3.  ビデオメモリマネージャーは、 *Updatepagetable*コマンドを使用して[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)を呼び出し、ページングプロセスページテーブルエントリをプロセス P ページテーブルとページディレクトリにマップします。
4.  ビデオメモリマネージャーは、 *Flushtlb (PagingProcessRootPageTable)* コマンドを使用して[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)を呼び出します。
5.  ビデオメモリマネージャーは、 *Updatepagetable*コマンドを使用して[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)を呼び出し、プロセスページのテーブルエントリに物理的な住所情報を格納します。
6.  ビデオメモリマネージャーは、 *Flushtlb (Process P root page table)* コマンドを使用して[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)を呼び出します。
7.  ページングバッファーは、ページングプロセスコンテキストで実行するために送信されます。

![プロセスのページテーブルエントリを更新しています](images/examples.1.png)

## ある場所から別の場所への割り当てコンテンツの転送<a name="transferring-allocation-content-from-one-location-to-another"></a>


次に、割り当てコンテンツをある場所から別の場所に転送する場合の一連の操作を示します ( ローカルメモリからシステムメモリ) にします。

1.  ビデオメモリマネージャーは、ソース割り当てとターゲット割り当ての仮想アドレス範囲を、ページングプロセス仮想アドレススクラッチ領域に割り当てます。
2.  ビデオメモリマネージャーは、 *Updatepagetable*コマンドを使用して[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)を呼び出します。 このコマンドは、ソース仮想アドレス範囲のページングプロセスページテーブルエントリを、ローカル GPU メモリ内の割り当て物理アドレスにマップします。
3.  ビデオメモリマネージャーは、 *Updatepagetable*コマンドを使用して[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)を呼び出します。 このコマンドは、宛先仮想アドレスのページングプロセスページテーブルエントリをシステムメモリにマップします。
4.  ビデオメモリマネージャーは、 *Flushtlb (ページングプロセスルートページテーブル)* を使用して[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)を呼び出します。
5.  ビデオメモリマネージャーは、転送操作を実行するために、 *Transfervirtual*コマンドを使用して[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)を呼び出します。
6.  ページングバッファーは、ページングプロセスコンテキストで実行するために GPU に送信されます。

![ある場所から別の場所への割り当てコンテンツの転送](images/examples.2.png)

## パターンを使用した割り当ての塗りつぶし<a name="filling-an-allocation-with-a-pattern"></a>


パターンを使用して割り当てを設定する必要がある場合の一連の操作を次に示します。

1.  ビデオメモリマネージャーは、ページングプロセス仮想アドレススクラッチ領域に、宛先割り当ての仮想アドレス範囲を割り当てます。
2.  ビデオメモリマネージャーは、 *Updatepagetable*コマンドを使用して[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)を呼び出します。 コマンドは、接続先の仮想アドレスのページングプロセスページテーブルエントリをマップします。
3.  ビデオメモリマネージャーは、 *Flushtlb (ページングプロセスルートページテーブル)* を使用して[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)を呼び出します。
4.  ビデオメモリマネージャーは、 *Fillvirtual*コマンドを使用して[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)を呼び出し、操作を実行します。
5.  ページングバッファーは、ページングプロセスコンテキストで実行するために GPU に送信されます。

![パターンを使用した割り当ての塗りつぶし](images/examples.3.png)

## <a name="making-an-allocation-resident-in-system-memory"></a>システムメモリに割り当てを常駐させる


割り当てを常駐させるために[**D3DKMTMakeResident**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtmakeresident)を呼び出すと、次の操作が実行されます。 アプリケーションプロセスのページテーブルがメモリに常駐していることを前提としています。

アプリケーションスレッドコンテキストで、次のようにします。

1.  割り当て仮想アドレス範囲の物理システムメモリページを割り当ててピン留めします (割り当てがシステムメモリに常駐している場合)。
2.  アプリケーションデバイスの新しいページングフェンス ID を生成します。
3.  [**Makeresident**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtmakeresident)コマンドを video memory manager の作業スレッドに送信します。
4.  アプリケーションに戻ります。

Video memory manager ワーカースレッドコンテキストで、次のようにします。

1.  アプリケーションプロセスページのテーブルエントリを更新します (上記の対応するセクションを参照してください)。
2.  割り当てがローカルメモリセグメントに存在する場合は、割り当てに0を入力します (上記の対応するセクションを参照してください)。
3.  ページングフェンス ID を使用して、 *Signal同期オブジェクト*コマンドをスケジューラに送信します。

## <a name="initialization-of-the-memory-manager-control-structures"></a>メモリマネージャーのコントロール構造体の初期化


<span id="The_paging_process_initialization"></span><span id="the_paging_process_initialization"></span><span id="THE_PAGING_PROCESS_INITIALIZATION"></span>ページングプロセスの初期化  

Microsoft DirectX グラフィックスカーネルは、グラフィックスデバイスが*D0*電力デバイス状態に切り替わったときに、ページングプロセス仮想アドレス空間を初期化します。

1.  ページングプロセスは[*DxgkDdiCreateProcess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createprocess)を使用して作成されます。
2.  システムデバイスは、 [*DxgkDdiCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)を使用して作成されます。 この時点で、カーネルモードドライバーは、ページングプロセスのアドレス空間に仮想アドレス範囲を予約できます。
3.  ページテーブルの割り当ては、ページングプロセス用に作成されます。
4.  ページテーブルの割り当ては、仮想アドレス指定機能の構造で定義されているメモリセグメントにコミットされます。
5.  [*Updatepagetable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)操作は、ページテーブルを初期化するために呼び出されます。

<span id="A_client_process_initialization"></span><span id="a_client_process_initialization"></span><span id="A_CLIENT_PROCESS_INITIALIZATION"></span>クライアントプロセスの初期化  

新しいプロセスが作成されると、DirectX のグラフィックスカーネルは次のようになります。

-   ページテーブルの初期割り当てを作成します。
-   プロセスからの最初の割り当てが行われたときに、ページテーブルの割り当てを初期化します。

 

 

