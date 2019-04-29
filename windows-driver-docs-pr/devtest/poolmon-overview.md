---
title: PoolMon の概要
description: PoolMon の概要
ms.assetid: c540e156-f0ce-4ac2-88e3-2e199b513abe
keywords:
- PoolMon WDK、PoolMon について
- メモリ プール モニタについての WDK のメモリ プール モニタ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87fe77831ccf023913b3e74fc37370f0dc97d6a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327258"
---
# <a name="poolmon-overview"></a>PoolMon の概要


## <span id="ddk_poolmon_overview_tools"></span><span id="DDK_POOLMON_OVERVIEW_TOOLS"></span>


PoolMon では、メモリの割り当てに関する次のデータを表示します。 データは、割り当てのプール タグを使用して並べ替えられます。

-   割り当て操作と無料の操作 (と未解放のメモリの割り当て) の数。

-   割り当て操作と更新プログラムの間の無料の操作の数を変更します。

-   使用すると、バイト単位でのタグを使用してメモリの割り当ての合計サイズと割り当ての平均サイズ。

-   更新プログラムの間でサイズをバイト単位で変更します。

-   このドライバーは、タグの値を割り当てます。

PoolMon には、合計および使用可能なメモリ、ページ フォールト、カーネルの物理メモリ、コミットされたメモリと、commit limit、ピーク時のメモリ ページおよび非ページ プールのサイズなど、全般的なメモリの情報も表示されます。

PoolMon を使用することもできます。

-   並べ替えと reconfigure、PoolMon は、実行中に表示します。

-   構成されているデータをファイルに保存します。

-   ローカル システム (32 ビット Windows のみ) でのドライバーによって使用されるタグのファイルを生成します。

 

 





