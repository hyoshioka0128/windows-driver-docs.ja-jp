---
title: システム ページング プロセス
description: ほとんどのページング操作は、システムのページングのプロセスのコンテキストで発生します。 唯一の例外は、付属の特別なコンテキストで行われ、レンダリングの同期が発生した UpdateGpuVirtualAddress コールバックからのページ テーブルの更新。
ms.assetid: B010C7E5-6B67-43D2-92A6-5258B132FB5D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0066a414d3f93a2ae039dbdc64aa4717cf033b0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372034"
---
# <a name="system-paging-process"></a>システム ページング プロセス


ほとんどのページング操作は、システムのページングのプロセスのコンテキストで発生します。 唯一の例外はからページ テーブルの更新、 [ *UpdateGpuVirtualAddress コールバック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_updategpuvirtualaddresscb)付属の特別なコンテキストで発生してレンダリングの同期が発生します。

Microsoft DirectX グラフィックスのカーネルは、ように、ページング操作を実行するのにシステムのページングのプロセスを使用します。

-   システムとローカルのグラフィックス処理ユニット (GPU) のメモリの割り当てを転送します。
-   塗りつぶしのパターンを持つ割り当て
-   ページのテーブルを更新します。
-   割り当てを絞りセグメントにマップします。
-   変換ルックア サイド バッファーをフラッシュします。

ページング プロセスは、独自の GPU 仮想アドレス空間、GPU のコンテキストとダイレクト メモリ アクセス (DMA) バッファー (呼び出されたページング バッファー) にします。 物理メモリに固定されてし、電源の遷移中にのみ削除は、独自のページ テーブルがあります。

ページングのプロセス仮想アドレス空間は、定義済みのレイアウトには、アダプターの初期化、およびメモリの内容が電源の切り替えにより失われた後に毎回の中に初期化されます。

![仮想および物理アドレス空間](images/system-paging-process.1.png)

DirectX グラフィックスのカーネルには、十分なページ テーブルと 1 GB の仮想アドレス空間をカバーするルート ページ テーブル内のページ テーブル エントリを初期化します。 スクラッチ領域では、ページングのプロセス仮想アドレス空間を転送および塗りつぶしの操作中に一時的に使用されるマップの割り当てです。 割り当てが仮想アドレスのスクラッチ領域に収まらない場合、転送操作はチャンクで行われます。

ページングのプロセスではシステム ルート ページ テーブルの割り当てが作成されます。 その内容は、初期化とことはありません (電源が遷移した後を除く) の変更時に設定されます。

システム プロセスのページ テーブルは、2 つの部分に分けられます。

A*システム ページ テーブル*が作成されますが反映されます、*スクラッチ領域ページ テーブル*システム プロセスのアドレス空間にします。 これには、スクラッチ領域ページ テーブルを変更して、必要に応じて、スクラッチ領域からメモリをマップまたはマップ解除するシステム プロセスができるようにします。 ページ テーブルの内容は、アダプターの初期化中に設定され、決して変化します。
*スクラッチ領域ページ テーブル*ページ テーブル エントリを使用して割り当てをページング プロセスの仮想アドレス空間にマップします。 として初期化される*無効な*初期化中に、ページング操作の後で使用します。
ページング処理のページ テーブルで初期化[ *UpdatePageTable* ](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)ページング アダプターの初期化と電源オン イベント時に操作します。 これらの操作に対して、 **PageTableUpdateMode**が強制的に**CPU\_仮想**(ページング バッファーを使用しない必要があります)、CPU を使用してすぐに完了する必要があります。

他のすべてのプロセスのページ テーブル エントリの更新を実行を使用して、 **PageTableUpdateMode**ドライバーで指定します。 これらの更新プログラムは、ページング プロセスのコンテキストで実行されます。

次に、セットアップを実行する方法を示します。

1.  1 GB のアドレス領域をカバーするには、ルート ページ テーブルの割り当てと下位レベルのページ テーブルの割り当てが作成されます。
2.  割り当ては、メモリのセグメントにコミットされます。
3.  複数[ *UpdatePageTable* ](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)ページ テーブル エントリを初期化するために、ドライバーにページング操作が発行されます。

ページング プロセス仮想アドレス領域の初期化の例として、次のパラメーターの場合を考えてみましょう。

-   ページ サイズは 4096 バイトです。
-   1 GB は、プロセス仮想アドレス空間のページング
-   ページ テーブル エントリのサイズは 4 バイトです。

この場合から成る 2 レベルの変換スキーム必要があります。

-   1 つのシステム ルート ページ テーブル
-   1 つのシステム ページ テーブル
-   255 のスクラッチ領域ページ テーブル

次の図は、ルート ページのテーブルと物理メモリ内のページ テーブルの場所に基づくはページのテーブルの初期化方法を示します。 図としてのみ、物理アドレスが指定されているに注意してください。
ページのテーブルでは、4 MB のアドレス領域について説明します。 したがって、システム ページ テーブルには、スクラッチ領域 ページのすべてのテーブルについて説明します。 スクラッチ領域は、4 MB の仮想アドレスから開始します。

ように、0 ~ 4095 の仮想アドレス範囲が有効になります。

![ページ テーブルの初期化](images/system-paging-process.2.png)

 

 





