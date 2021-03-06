---
title: プロセス常駐の予算
description: Windows Display Driver Model (WDDM) v2 では、メモリの量を維持できる常駐の予算のプロセスが割り当てられます。
ms.assetid: 9A93E110-4D3F-4D08-8379-222A2D7DEFBB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 774f0fd2a8a04dd7de35d3228d68efa76c0b349a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363710"
---
# <a name="process-residency-budgets"></a>プロセス常駐の予算


Windows Display Driver Model (WDDM) v2 では、メモリの量を維持できる常駐の予算のプロセスが割り当てられます。 この予算では、時間の経過と共に変更できますが、通常はのみが適用されるとき、システムがメモリ不足。 Microsoft direct3d12 では、前に、予算がの形式では、ユーザー モード ドライバーによって処理される*トリミング*通知と*MakeResident*によるエラー**状態\_ありません\_メモリ**します。 *TrimToBudget*通知、 [*削除*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_evictcb)、および失敗した[ *MakeResident* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb)で最新の予算を返すすべての呼び出し、整数のフォーム**NumBytesToTrim**新しい予算に適合するためにトリミングする必要がある量を示す値です。

Direct3d12 のアプリケーションでは、予算は、アプリケーションで完全に処理します。 キューと、予算のサイズは、アプリケーションをそれ自体のサイズを把握できるようにします。 予算のサイズをヒントとして使用すると、アプリケーションが常駐、どのような解像度と質のリソースを保持するリソースの数を決定できます。

これらの予算を正しく管理するには、カーネルの予算にどのようなメモリが参加する必要がありますを把握する必要があります。 新しい**ApplicationTarget**ビット[ **DXGK\_SEGMENTFLAGS2** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxgk-segmentflags2)カーネル モード ドライバーにすることを希望しているセグメント上に設定する必要がある構造体予算のロジックに含まれます。 たとえば、VRAM の 1 つのセグメントを持つ独立したグラフィックス処理装置 (GPU) でを用のアプリケーションの使用状況、および VRAM のために使用される専用のリソースに自動的に、ドライバーはとして可能性がありますのみマークプライマリVRAMをセグメント化の1セグメント**ApplicationTarget**します。 統合の Gpu のメイン aperture セグメントがマークされている 1 つを通常になります。 としてマークできるセグメントの数に制限はありません**ApplicationTarget**します。 カーネルは、これらを組み合わせて集計を統一されたサイズを使用してアプリケーションを表示します。

 

 





