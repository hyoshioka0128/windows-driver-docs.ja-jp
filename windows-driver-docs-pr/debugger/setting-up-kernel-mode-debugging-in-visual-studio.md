---
title: Visual Studio でのカーネル モード デバッグの設定
description: Microsoft Visual Studio を使用すると、Windows のカーネルモードデバッグをセットアップして実行できます。
ms.assetid: 38E57F45-71D9-4467-BECF-42769563751E
keywords:
- カーネルモードのデバッグ、Visual Studio
- カーネルモードデバッグのセットアップ、Visual Studio
ms.date: 04/10/2017
ms.localizationpriority: medium
ms.openlocfilehash: 205321c0957b89983fc63a53be876d6d44482982
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534761"
---
# <a name="span-iddebuggersetting_up_kernel-mode_debugging_in_visual_studiospansetting-up-kernel-mode-debugging-in-visual-studio"></a><span id="debugger.setting_up_kernel-mode_debugging_in_visual_studio"></span>Visual Studio でのカーネル モード デバッグの設定

> [!IMPORTANT]
> この機能は、Windows 10 バージョン1507以降のバージョンの WDK では使用できません。
>


Microsoft Visual Studio を使用すると、Windows のカーネルモードデバッグをセットアップして実行できます。 Visual Studio を使用してカーネルモードのデバッグを行うには、Visual Studio に Windows Driver Kit (WDK) が統合されている必要があります。 統合環境をインストールする方法の詳細については、「 [Visual Studio を使用したデバッグ](debugging-using-visual-studio.md)」を参照してください。
 

Visual Studio を使ってカーネル モード デバッグをセットアップするのではなく、手動でセットアップすることができます。 詳細については、「[カーネルモードデバッグの手動](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)セットアップ」を参照してください。

カーネルモードのデバッグには、通常、2台のコンピューターが必要です。 デバッガーは*ホストコンピューター*上で実行され、デバッグ中のコードは*対象のコンピューター*上で実行されます。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


-   [Visual Studio でのネットワーク ケーブル経由でのカーネルモード デバッグの設定](setting-up-a-network-debugging-connection-in-visual-studio.md)
-   [Visual Studio での 1394 ケーブル経由でのカーネルモード デバッグの設定](setting-up-a-1394-cable-connection-in-visual-studio.md)
-   [Visual Studio での USB 3.0 ケーブル経由でのカーネルモード デバッグの設定](setting-up-a-usb-3-0-cable-connection-in-visual-studio.md)
-   [Visual Studio での USB 2.0 ケーブル経由でのカーネルモード デバッグの設定](setting-up-a-usb-2-0-cable-connection-in-visual-studio.md)
-   [Visual Studio でのシリアル ケーブル経由でのカーネルモード デバッグの設定](setting-up-a-null-modem-cable-connection-in-visual-studio.md)
-   [Visual Studio での USB 経由のシリアル接続を使ったカーネル モード デバッグの設定](setting-up-kernel-mode-debugging-using-serial-over-usb-in-visual-studio.md)
-   [Visual Studio での仮想マシンのカーネルモード デバッグの設定](setting-up-a-connection-to-a-virtual-machine-in-visual-studio.md)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[デバッグの設定 (カーネルモードとユーザーモード)](getting-set-up-for-debugging.md)

[カーネル モードのデバッグを手動でセットアップする](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

 

 






