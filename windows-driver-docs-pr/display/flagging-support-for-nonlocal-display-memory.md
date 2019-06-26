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
ms.openlocfilehash: 2add9d7236d29610953c4499d93ede46c7ed47b2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385817"
---
# <a name="flagging-support-for-nonlocal-display-memory"></a>非ローカルの表示メモリに対するフラグ設定のサポート


## <span id="ddk_flagging_support_for_nonlocal_display_memory_gg"></span><span id="DDK_FLAGGING_SUPPORT_FOR_NONLOCAL_DISPLAY_MEMORY_GG"></span>


ドライバーは、DirectDraw を通知する必要があります (と DirectDraw アプリケーション) AGP 互換であります。 これは、機能を指定することによって実現されますビット DDCAPS2\_で NONLOCALVIDMEM、 **dwCaps2**のメンバー、 [ **DDCORECAPS** ](https://docs.microsoft.com/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)一部である構造体[ **DD\_HALINFO** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo) DirectDraw に構造体が渡されます。

DirectDraw をオフ、DDCAPS2 AGP サービスをサポートしないオペレーティング システムで実行して場合、\_NONLOCALVIDMEM 機能ビットとすべての関連付けられた非ローカル ヒープ。

 

 





