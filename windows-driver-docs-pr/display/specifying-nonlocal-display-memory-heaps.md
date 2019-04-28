---
title: 非ローカルの表示メモリ ヒープの指定
description: 非ローカルの表示メモリ ヒープの指定
ms.assetid: 4320b6e7-81ef-4bb4-bda8-680467b6421f
keywords:
- ヒープ WDK DirectDraw
- ヒープ メモリ WDK の DirectDraw を表示します。
- WDK DirectDraw、ヒープの非ローカルの表示メモリ
- AGP WDK DirectDraw、ヒープ
- ヒープ AGP サポート WDK DirectDraw を描画するには、
- DirectDraw AGP サポート WDK Windows 2000 の表示、ヒープ
- WDK DirectDraw AGP、ヒープ メモリ
- 線形ヒープ WDK DirectDraw
- 物理的なヒープ WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d76dad4381703ce654ae57316690131a12338cd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376032"
---
# <a name="specifying-nonlocal-display-memory-heaps"></a>非ローカルの表示メモリ ヒープの指定


## <span id="ddk_specifying_nonlocal_display_memory_heaps_gg"></span><span id="DDK_SPECIFYING_NONLOCAL_DISPLAY_MEMORY_HEAPS_GG"></span>


DirectDraw ドライバー制御 AGP メモリの量利用可能で、どの画面でヒープを返すことによって、 [ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)つまり DirectDraw に渡されたバックを構造体します。 ドライバーの識別、VIDMEM を指定することで、非ローカル ヒープ\_ISNONLOCAL フラグ、 **dwFlags**のメンバー、 [**グラフィックスアクセラレータ**](https://msdn.microsoft.com/library/windows/hardware/ff570171)データ構造体ヒープをについて説明します。 さらに、ドライバーが、VIDMEM を指定することで、非ローカル ヒープ上のメモリの書き込みの結合を有効にできます。\_VIDMEM に加えて ISWC フラグ\_ISNONLOCAL します。

サイズ (線形または四角形)、(結合書き込み) 属性、およびサーフェイスのタイプ、ヒープしないでし、使用することはできません、DirectDraw を記述する AGP と互換性のある DirectDraw ドライバーの役目です。 ただし、実際にしてヒープまたはコミット メモリのアドレス空間を予約するドライバーの責任ではありません。 これは、ドライバーの代わりに DirectDraw によって処理されます。 DirectDraw、ドライバーから AGP メモリの管理の詳細を非表示にします。

非表示のメモリ ヒープを指定するときに、ドライバーで指定された開始アドレスの意味はありません。 開始アドレス、線形および物理デバイス、非ローカル ヒープのテーブル (GART) を再マップ両方グラフィックのアドレスは、DirectDraw がヒープを作成することを要求したときに、オペレーティング システムによって決まります。 そのため、ドライバーは、開始アドレスのすべての値を返すことができます。 四角形のヒープでは、この開始アドレスは DirectDraw によって無視されます。 指定した幅と高さは、DirectDraw メモリ要件を決定する必要がありますではすべてです。 線形ヒープでは、開始アドレスは、ヒープのサイズを計算するために使用される範囲内にのみ、意味を持ちます。

DirectDraw (fpEnd - fpStart) での線形のヒープは + 1 (指定した終了アドレスが、ヒープの終了後の最初のバイトしない、ヒープの最後のバイトであることに注意してください) のサイズを決定します。 そのため、結果が、ヒープの最大サイズで DirectDraw では、終了アドレスからそのアドレスを減算し、1 を追加、ときに限り、任意の開始アドレスを指定できます。

のみ、物理メモリは AGP ヒープにコミットされます (つまり、サーフェスが割り当てられている) には、必要に応じて、これが非常に大規模な非ローカル ヒープを指定しないこと重要です。 このようなヒープは、共有のアドレス領域を消費され、物理メモリよりも前にその他の重要なリソースがコミットされます。

DirectDraw と Windows オペレーティング システムが特定の時点にコミットできる AGP メモリの量にポリシーの制限を課すことに注意してください。 重要です。 これは、システムの残りのリソースの枯渇を防ぐために必要です。 したがって、要求に失敗する場合でも、これを非ローカル ヒープ コミットされていない完全非ローカルの表示メモリ サーフェスの決しては。

DirectDraw、ヒープの正しいアドレス (線形、および物理) を特定したときにそのヒープ記述子でそれらを保存します。 DirectDraw には、これらのアドレスの初期化時に、ドライバーに通知するためのメカニズムも提供します。 これを行う方法は、特定のプラットフォームです。

-   Microsoft Windows 2000 以降、これは、 [ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404) GUID を使用して呼び出す\_UpdateNonLocalHeap GUID。 この GUID に渡された場合*DDGetDriverInfo*、ヒープ データが渡された、 [ **DD\_UPDATENONLOCALHEAPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551748)データ構造体。

 

 





