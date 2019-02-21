---
title: WDM オーディオの Windows Vista のサポート
description: WDM オーディオの Windows Vista のサポート
ms.assetid: a9cf1660-3757-4f8d-82c7-de654bddfb49
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d619ada8fae09ffebf40bc1afcd0220edeb4e8e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558815"
---
# <a name="windows-vista-support-for-wdm-audio"></a>WDM オーディオの Windows Vista のサポート


## <span id="windows_xp_support_for_wdm_audio"></span><span id="WINDOWS_XP_SUPPORT_FOR_WDM_AUDIO"></span>


Windows Vista には、次の WDM オーディオ機能がサポートされています。

-   WDM バージョン 1.40

-   次の例外が、Windows XP をサポートするすべての機能です。
    -   Windows Vista ミキサー API をアプリケーションごとのモードで実行する場合を除く、ハードウェアのピーク時のメーターがサポートされます。
    -   Wave と MIDI NT4 ドライバーが正常に機能しますが、新しいオーディオのユーザー インターフェイスでサポートされていません。
    -   AUX デバイスはサポートされていません、 [ **auxGetNumDevs** ](https://msdn.microsoft.com/library/windows/desktop/dd756713) Mmsystem.h 内の関数は常に 0 の数を返します。
    -   Windows NT4 スタイル ミキサー ドライバー (DRIVERS32) がサポートされていません。

 

 




