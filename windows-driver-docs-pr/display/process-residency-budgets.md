---
title: プロセス常駐の予算
description: Windows Display Driver Model (WDDM) v2 では、プロセスには、常駐可能なメモリの量に関する予算が割り当てられます。
ms.assetid: 9A93E110-4D3F-4D08-8379-222A2D7DEFBB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43f5c48df4c435c622de66e8015c2b423fa9b7b3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829689"
---
# <a name="process-residency-budgets"></a>プロセス常駐の予算


Windows Display Driver Model (WDDM) v2 では、プロセスには、常駐可能なメモリの量に関する予算が割り当てられます。 この予算は時間の経過と共に変化しますが、一般に、システムのメモリが不足している場合にのみ適用されます。 Microsoft Direct3D 12 より前のリリースでは、ユーザーモードドライバーによって、ユーザーモードドライバーによって、 *Trim*通知と、**状態\_\_メモリなし**の*makeresident*エラーの形式で処理されています。 *TrimToBudget* Notification、[*削除*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_evictcb)、および失敗した[*makeresident*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb)のすべての呼び出しは、新しい予算に適合するためにどのくらいの量を切り捨てる必要があるかを示す整数**numbytestotrim**値の形式で、最新の予算を返します。

Direct3D 12 アプリケーションの場合、予算はアプリケーションによって完全に処理されます。 予算のサイズは、アプリケーションがそれ自体のサイズを把握できるようにするための手掛かりとして使用されます。 コストのサイズをヒントとして使用することで、アプリケーションは、常駐させるリソースの数、保持するリソースの解決方法や品質を決定できます。

これらの予算を適切に管理するには、カーネルが予算に参加する必要があるメモリを把握しておく必要があります。 [**DXGK\_SEGMENTFLAGS2**](https://docs.microsoft.com/windows-hardware/drivers/display/dxgk-segmentflags2)構造体には、カーネルモードドライバーが予算ロジックに含まれるセグメントに設定する必要がある新しい**applicationtarget**ビットがあります。 たとえば、アプリケーションの使用に適した VRAM の1つのセグメントと、特別な目的のリソースに対して自動的に使用される VRAM の1つのセグメントを含む個別のグラフィックスプロセッシングユニット (GPU) では、ドライバーはプライマリ VRAM セグメント**をApplicationTarget**。 統合 Gpu の場合、メインのアパーチャセグメントは、通常はとマークされたものになります。 **Applicationtarget**としてマークできるセグメントの数に制限はありません。 カーネルはこれらをまとめて集計し、アプリケーションに統一されたサイズで表示します。

 

 





