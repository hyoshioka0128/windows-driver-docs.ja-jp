---
title: Windows Vista による WDM オーディオのサポート
description: Windows Vista による WDM オーディオのサポート
ms.assetid: a9cf1660-3757-4f8d-82c7-de654bddfb49
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3869361770c57ae4d447e5778f5dfa28a2eb9c26
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354087"
---
# <a name="windows-vista-support-for-wdm-audio"></a>Windows Vista による WDM オーディオのサポート


## <span id="windows_xp_support_for_wdm_audio"></span><span id="WINDOWS_XP_SUPPORT_FOR_WDM_AUDIO"></span>


Windows Vista には、次の WDM オーディオ機能がサポートされています。

-   WDM バージョン 1.40

-   次の例外が、Windows XP をサポートするすべての機能です。
    -   Windows Vista ミキサー API をアプリケーションごとのモードで実行する場合を除く、ハードウェアのピーク時のメーターがサポートされます。
    -   Wave と MIDI NT4 ドライバーが正常に機能しますが、新しいオーディオのユーザー インターフェイスでサポートされていません。
    -   AUX デバイスはサポートされていません、 [ **auxGetNumDevs** ](https://docs.microsoft.com/previous-versions/dd756713(v=vs.85)) Mmsystem.h 内の関数は常に 0 の数を返します。
    -   Windows NT4 スタイル ミキサー ドライバー (DRIVERS32) がサポートされていません。

 

 




