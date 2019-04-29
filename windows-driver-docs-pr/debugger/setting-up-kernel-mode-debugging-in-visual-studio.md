---
title: Visual Studio でのカーネル モード デバッグの設定
description: Microsoft Visual Studio を使用して、設定し、Windows のカーネル モードのデバッグを実行することができます。
ms.assetid: 38E57F45-71D9-4467-BECF-42769563751E
keywords:
- カーネル モードのデバッグ、Visual Studio
- カーネル モードのデバッグ、Visual Studio の設定
ms.date: 04/10/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7880050e1712a5daaa245dc8b0ae77b9cd2dcbc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335533"
---
# <a name="span-iddebuggersettingupkernel-modedebugginginvisualstudiospansetting-up-kernel-mode-debugging-in-visual-studio"></a><span id="debugger.setting_up_kernel-mode_debugging_in_visual_studio"></span>Visual Studio でのカーネル モード デバッグのセットアップ

> [!IMPORTANT]
> この機能は、Windows 10 バージョン 1507、以降のバージョンの WDK でご利用いただけません。
>


Microsoft Visual Studio を使用して、設定し、Windows のカーネル モードのデバッグを実行することができます。 カーネル モードのデバッグを Visual Studio を使用するには、Windows Driver Kit (WDK) の Visual Studio と統合が必要です。 統合環境をインストールする方法については、次を参照してください。 [Windows ドライバー開発](https://go.microsoft.com/fwlink/p?linkid=301383)します。
 

Visual Studio を使ってカーネル モード デバッグをセットアップするのではなく、手動でセットアップすることができます。 詳細については、次を参照してください。[カーネル モード デバッグ手作業でセットアップ](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)します。

カーネル モードのデバッグでは、2 台のコンピューター通常必要があります。 デバッガーを実行する、*ホスト コンピューター、* での実行をデバッグ対象のコードと、*ターゲット コンピューター*します。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


-   [Visual Studio でのネットワーク ケーブル経由でのカーネル モードのデバッグのセットアップ](setting-up-a-network-debugging-connection-in-visual-studio.md)
-   [Visual Studio で 1394 ケーブル経由でのカーネル モード デバッグの設定](setting-up-a-1394-cable-connection-in-visual-studio.md)
-   [カーネル モードの Visual Studio での 3.0 ケーブル、USB 経由でデバッグの設定](setting-up-a-usb-3-0-cable-connection-in-visual-studio.md)
-   [カーネル モードで Visual Studio 2.0 ケーブル、USB 経由でデバッグの設定](setting-up-a-usb-2-0-cable-connection-in-visual-studio.md)
-   [Visual Studio でのシリアル ケーブル経由でのカーネル モードのデバッグのセットアップ](setting-up-a-null-modem-cable-connection-in-visual-studio.md)
-   [カーネル モード デバッグのセットアップ シリアルを使用して、Visual Studio での USB 経由で](setting-up-kernel-mode-debugging-using-serial-over-usb-in-visual-studio.md)
-   [Visual Studio での仮想マシンのカーネル モード デバッグのセットアップ](setting-up-a-connection-to-a-virtual-machine-in-visual-studio.md)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[デバッグ (カーネル モードとユーザー モード) の設定](getting-set-up-for-debugging.md)

[カーネル モードのデバッグを手動での設定](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

 

 






