---
title: 非ローカルの表示メモリに対するフラグ設定のサポート
description: 非ローカルの表示メモリに対するフラグ設定のサポート
ms.assetid: 5e5187e8-ff93-48e0-997d-71d65d35757f
keywords:
- メモリ WDK DirectDraw、互換表示します。
- WDK DirectDraw、互換性の非ローカルの表示メモリ
- AGP WDK DirectDraw、互換性
- 描画 AGP サポート WDK DirectDraw、互換性
- DirectDraw AGP サポート WDK Windows 2000 の表示の互換性
- WDK DirectDraw AGP、互換性のメモリ
- WDK DirectDraw の互換性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88fb1aa3c5a2faaa092392b2b70f5dc92b491627
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347580"
---
# <a name="flagging-support-for-nonlocal-display-memory"></a>非ローカルの表示メモリに対するフラグ設定のサポート


## <span id="ddk_flagging_support_for_nonlocal_display_memory_gg"></span><span id="DDK_FLAGGING_SUPPORT_FOR_NONLOCAL_DISPLAY_MEMORY_GG"></span>


ドライバーは、DirectDraw を通知する必要があります (と DirectDraw アプリケーション) AGP 互換であります。 これは、機能を指定することによって実現されますビット DDCAPS2\_で NONLOCALVIDMEM、 **dwCaps2**のメンバー、 [ **DDCORECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549248)一部である構造体[ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627) DirectDraw に構造体が渡されます。

DirectDraw をオフ、DDCAPS2 AGP サービスをサポートしないオペレーティング システムで実行して場合、\_NONLOCALVIDMEM 機能ビットとすべての関連付けられた非ローカル ヒープ。

 

 





