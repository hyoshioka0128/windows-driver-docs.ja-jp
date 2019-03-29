---
title: デュアル ブート コンピューターのデバッグ
description: デュアル ブート コンピューターのデバッグ
ms.assetid: 46ed532e-5ef3-4893-b2eb-da8eb52121f0
keywords:
- デュアル ブート コンピューター
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9a503eb04f9af739fb0f53fedfa826820787745
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574058"
---
# <a name="debugging-a-dual-boot-machine"></a>デュアル ブート コンピューターのデバッグ


## <span id="ddk_debugging_dual_boot_machines_dbg"></span><span id="DDK_DEBUGGING_DUAL_BOOT_MACHINES_DBG"></span>


デュアル ブート コンピューターで別のオペレーティング システムが起動しない場合の応答方法

最初に、ブート オプションを指す、他のオペレーティング システムのパスが正しいことを確認します。 参照してください[を取得する設定をデバッグ用](getting-set-up-for-debugging.md)詳細についてはします。

X86 コンピューターも確認してくださいその boosect.ini が存在します。 このファイルには、その他のオペレーティング システムのブート レコードが含まれています。 このファイルを再表示するには、使用、 **attrib-r-s-h boosect.ini**コマンド。

 

 





