---
title: ハードウェアからの 3-D 仮想テクスチャの直接操作
description: ハードウェアからの 3-D 仮想テクスチャの直接操作
ms.assetid: 5390f62d-3359-4f19-ab6c-07239e598b20
keywords:
- 3 次元テクスチャ WDK を表示します。
- テクスチャの WDK の表示
- 3-D テクスチャ WDK の表示
- 3-D を操作するテクスチャ WDK 表示では直接
- ハードウェア 3-D テクスチャ操作 WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac13da25f91a0590623def4866f44f0d83e62869
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581349"
---
# <a name="manipulating-3-d-virtual-textures-directly-from-hardware"></a>ハードウェアからの 3-D 仮想テクスチャの直接操作


## <span id="ddk_manipulating_3_d_virtual_textures_directly_from_hardware_gg"></span><span id="DDK_MANIPULATING_3_D_VIRTUAL_TEXTURES_DIRECTLY_FROM_HARDWARE_GG"></span>


ユーザー モードのディスプレイ ドライバーは、既存の仮想アドレス (たとえば、3 次元 (3 D) テクスチャ ファイルのビューの仮想アドレス) の上に割り当てを作成できます。 3-D テクスチャをシステム メモリのコピーを使用したハードウェアの操作を使用できるように既存の仮想アドレスの上に割り当てを作成します。 ただし、このシナリオでは、ユーザー モード表示、ドライバーの*ロック*仮想アドレスの割り当てでは、ビデオ メモリによって割り当てられていないために、関数はシステム メモリにローカルのビデオ メモリからページを削除常にする必要がありますマネージャー。 そのため、ビデオ メモリ マネージャーは、透過的にビデオ メモリをその逆に、システム メモリからのテクスチャの仮想アドレスをマップし直すことはできません。 つまり、このプロパティを使用して仮想アドレスでは、マップ表示をすることはできません。

 

 





