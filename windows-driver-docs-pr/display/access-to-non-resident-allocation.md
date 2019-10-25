---
title: 非常駐割り当てへのアクセス
description: 常駐していない割り当てへの GPU アクセスは無効なため、エラーを生成したアプリケーションに対してデバイスが削除されます。
ms.assetid: 698ECD53-861A-4750-B33C-DF0611B87829
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f4961bb11378654c5d1c7219bfe11f900161a9e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839085"
---
# <a name="span-iddisplayaccess_to_non-resident_allocationspanaccess-to-non-resident-allocation"></a><span id="display.access_to_non-resident_allocation"></span>非常駐割り当てへのアクセス


グラフィックス処理ユニット (GPU) が常駐していない割り当てへのアクセスは無効なため、エラーを生成したアプリケーションに対してデバイスが削除されます。

障害が発生したエンジンが GPU 仮想アドレス指定をサポートしているかどうかによって、このような無効なアクセスを処理する2つの異なるモデルがあります。

-   GPU 仮想アドレス指定をサポートしておらず、割り当てとパッチの場所の一覧を使用してメモリ参照を修正するエンジンの場合、無効なアクセスは、ユーザーモードドライバーが割り当てリストを送信するときに、デバイス (つまり、ユーザーモードドライバーはその割り当てで[*MakeResidentCb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb)を呼び出していません)。 このようにすると、グラフィックスカーネルによって、問題のあるコンテキストまたはデバイスのエラーが発生します。
-   GPU 仮想アドレスがサポートされていても、無効な GPU 仮想アドレスにアクセスするエンジンの場合、仮想アドレスの背後に割り当てられていないか、有効な割り当てが存在するが、まだ常駐していないため、GPU は割り込みの形式での回復不可能なページフォールト。 ページフォールト割り込みが発生した場合、カーネルモードドライバーは、新しいページフォールト通知を使用してグラフィックスカーネルにエラーを転送する必要があります。 この通知を受信すると、グラフィックスカーネルによって、障害が発生したエンジンでエンジンのリセットが開始され、エラーが発生したコンテキストまたはデバイスのエラーが発生します。 エンジンのリセットが失敗した場合、グラフィックスカーネルは、完全なアダプター全体のタイムアウト検出と復旧 (TDR) にエラーを昇格させます。

 

 





