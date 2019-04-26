---
title: デバッグの設定 (カーネルモードとユーザーモード)
description: Windows デバッガーでのデバッグを設定できます 2 つの方法はあります。
ms.assetid: 3575B850-A0F9-4AAE-9432-E970D40069D2
keywords:
- デバッグのセットアップ
- デバッグを構成します。
- デバッガーを構成します。
- WinDbg
- Visual Studio のデバッグ
- カーネル モードのデバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5da0b40de3c66b1d3711218749503bef2ce3ac2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356672"
---
# <a name="setting-up-debugging-kernel-mode-and-user-mode"></a>デバッグの設定 (カーネルモードとユーザーモード)


Windows デバッガーでのデバッグを設定できます 2 つの方法はあります。 Microsoft Visual Studio (Windows Driver Kit (WDK) との統合) を使用することも、セットアップを手動で行うことができます。 カーネル モードのデバッグを設定した後は、デバッグ セッションを確立するために Visual Studio や WinDbg、KD を使用することができます。 ユーザー モードのデバッグを設定した後は、デバッグ セッションを確立するために Visual Studio、WinDbg、CDB、NTSD またはを使用できます。

**注**  ツールを Windows のデバッグに、Windows のデバッガーが含まれます。 次のデバッガーは、Visual Studio に含まれている Visual Studio デバッガーでは、異なるです。 詳細については、次を参照してください。 [Windows デバッグ](index.md)します。

 

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


-   [カーネル モードのデバッグを手動での設定](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)
-   [Windows 10 でのデバッグ ネットワーク カーネルのイーサネット Nic をサポート](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)
-   [Windows 8.1 でのデバッグ ネットワーク カーネルのイーサネット Nic をサポート](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)
-   [Windows 8 でのデバッグ ネットワーク カーネルのイーサネット Nic をサポート](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8.md)
-   [Visual Studio でのユーザー モード デバッグのセットアップ](setting-up-user-mode-debugging-in-visual-studio.md)
-   [バーチャル マシン ホストのネットワークのデバッグの設定](setting-up-network-debugging-of-a-virtual-machine-host.md)
-   [Tools.ini を構成します。](configuring-tools-ini.md)
-   [Using KDbgCtrl](using-kdbgctrl.md)

 

 





