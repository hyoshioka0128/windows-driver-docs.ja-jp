---
title: 非常駐割り当てへのアクセス
description: 常駐ではない割り当てへの GPU アクセスは無効であり、エラーを生成したアプリケーションの削除、デバイスになります。
ms.assetid: 698ECD53-861A-4750-B33C-DF0611B87829
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e04cdf46f6401eeb871296783540e178451b1375
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373598"
---
# <a name="span-iddisplayaccesstonon-residentallocationspanaccess-to-non-resident-allocation"></a><span id="display.access_to_non-resident_allocation"></span>非常駐割り当てへのアクセス


グラフィックス プロセッシング ユニット (GPU) への常駐ではない割り当ては無効であり、エラーを生成したアプリケーションの削除、デバイスになります。

これには、エラーが発生したエンジンがかどうかを示す仮想 GPU をサポートするかどうかに依存するこのような無効なアクセスの処理の 2 つの異なるモデルがあります。

-   ユーザー モード ドライバーに存在することはない割り当てを参照する割り当てリストを送信するときに不正なアクセスが発生しない GPU 仮想アドレス指定をサポートし、割り当てとメモリ参照の修正プログラムに修正プログラムの場所のリストを使用するエンジンの場合、デバイス (つまり、ユーザー モード ドライバーと呼ばれる[ *MakeResidentCb* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb)その割り当てに)。 この場合、グラフィックスのカーネルはエラーで欠陥のあるコンテキスト/デバイスを配置します。
-   エンジンの GPU 仮想アドレス指定をサポートせず、無効な GPU 仮想アドレスにアクセスする場合か、仮想アドレスの割り当てはありませんが、有効な割り当てはまたは常駐が作成されていないため、GPU は、発生が予想される、割り込みの形式で復旧不可能なページ フォールトします。 ページ フォールトの割り込みが発生したときに、カーネル モード ドライバーは新しいページ フォールト通知によるグラフィックス カーネルにエラーを転送する必要があります。 受信するとこの通知、グラフィックス カーネルは、エンジンを開始するエラー状態のエンジンをリセットおよび欠陥のあるコンテキスト/デバイスのエラーに。 エンジンのリセットが成功しなかった場合、グラフィックスのカーネルはフル アダプター全体のタイムアウト検出と復旧 (TDR) をすると、エラーを昇格します。

 

 





