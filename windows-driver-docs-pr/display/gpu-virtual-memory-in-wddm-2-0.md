---
title: WDDM 2.0 の GPU 仮想メモリ
description: このセクションでは、変更を行った理由も含めて、GPU の仮想メモリとドライバーが使用する方法の詳細を提供します。
ms.assetid: 88A99A31-9B84-4594-8A93-1C2783F7390D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4a848311cbb7e802b970bcc11598e9d96a23f90
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331289"
---
# <a name="gpu-virtual-memory-in-wddm-20"></a>WDDM 2.0 の GPU 仮想メモリ


このセクションでは、変更を行った理由も含めて、GPU の仮想メモリとドライバーが使用する方法の詳細を提供します。 この機能は、Windows 10 以降から使用できます。

## <a name="span-idintroductionspanspan-idintroductionspanspan-idintroductionspanintroduction"></a><span id="Introduction"></span><span id="introduction"></span><span id="INTRODUCTION"></span>概要


Windows Display Driver Model (WDDM) v1.x、グラフィックス処理ユニット (GPU) エンジンが予想されるセグメントの物理アドレスによってメモリを参照するよう、デバイス ドライバー インターフェイス (DDI) が構築されています。 セグメントでは、アプリケーション間で共有され、コミットを超える、リソースの配置がその有効期間を通じてとその割り当てられた物理アドレスを変更します。 これは、割り当てと修正プログラムの場所の一覧をコマンド バッファー内のメモリ参照を追跡し、そのバッファーを GPU エンジンに送信する前に適切な物理メモリの参照にパッチを適用する場合に、必要性につながります。 この追跡とコストが、基本的に、ビデオ メモリ マネージャーが、エンジンに送信する前に、すべてのパケットを検査、スケジューリング モデルは、修正プログラムの適用。

ハードウェア ベンダーの詳細については、モデル、GPU にユーザー モードから直接作業が送信されを検査するビデオ メモリ マネージャーの必要性を排除する必要がある GPU は、作業自体のさまざまなキューを管理、場所、ハードウェア ベースのスケジュール設定に移行するにし、すべてのコマンド バッファーを GPU エンジンに送信する前に修正プログラムを適用します。

これを実現するには、WDDM v2 でアドレス指定が仮想 GPU のサポートが導入されています。 このモデルでは、すべて GPU コンテキストで実行する、一意の GPU 仮想アドレス空間が各プロセスに割り当てられているを取得します。 作成または開いたのプロセスで、割り当て、割り当ての有効期間にわたって定数と一意のままそのプロセス GPU 仮想アドレス領域内で一意の GPU 仮想アドレスが割り当てられます。 これにより、GPU の仮想アドレスによる参照の割り当てをユーザー モード ドライバーを使用して、基になる物理メモリの有効期間を通じて変更について心配する必要はありません。

GPU の個々 のエンジンは、物理または仮想モードで動作できます。 物理のモードで、スケジューリング モデルは変わりません WDDM v1.x を使用します。 物理モード、ユーザー モード ドライバーは、割り当てを生成し、場所のリストを更新プログラムが続行されます。 コマンド バッファーに送信され、エンジンに送信する前に、実際の物理アドレスへのパッチ コマンド バッファーに提供されます。

仮想モードでは、エンジンは、GPU の仮想アドレスによってメモリを参照します。 このモードでは、ユーザー モード ドライバーは、ユーザー モードから直接コマンド バッファーを生成し、新しいサービスを使用して、カーネルにこれらのコマンドを送信します。 このモードでは、ユーザー モード ドライバーは割り当てを生成またはがまだ割り当ての保存場所を管理する場所のリスト、修正プログラムを適用します。 ドライバーの保存場所の詳細については、次を参照してください。 [WDDM 2.0 でのドライバーの常駐](driver-residency-in-wddm-2-0.md)します。

## <a name="span-idgpumemorymodelsspanspan-idgpumemorymodelsspanspan-idgpumemorymodelsspangpu-memory-models"></a><span id="GPU_memory_models"></span><span id="gpu_memory_models"></span><span id="GPU_MEMORY_MODELS"></span>GPU メモリ モデル


WDDM v2 は、GPU 仮想アドレス指定するための 2 つの異なるモデルをサポートしている*GpuMmu*と*IoMmu*します。 ドライバーをする必要がありますオプトイン モデルの一方または両方をサポートするためにします。 GPU の単一のノードでは、同時に両方のモードをサポートできます。

<span id="GpuMmu_model"></span><span id="gpummu_model"></span><span id="GPUMMU_MODEL"></span>GpuMmu モデル  
*GpuMmu* GPU メモリ管理ユニットと基になるページにビデオ メモリ マネージャーが管理モデル、テーブル、および割り当てに GPU 仮想アドレスのマッピングを管理できるようにするには、ユーザー モード ドライバー サービスを公開します。

詳細については、次を参照してください。 [GpuMmu モデル](gpummu-model.md)します。

<span id="IoMmu_model"></span><span id="iommu_model"></span><span id="IOMMU_MODEL"></span>IoMmu モデル  
*IoMmu*モデル、CPU と GPU は、一般的なアドレス空間とページ テーブルを共有します。

詳細については、次を参照してください。 [IoMmu モデル](iommu-model.md)します。

 

 





