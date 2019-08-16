---
ms.assetid: 2274e848-2a0b-445c-82cd-7bcd9e23078a
title: ドライバーのデバッグ
description: 通常、カーネル モード ドライバーのデバッグには、2 台のコンピューターが必要です。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c325b9b4400c52c30e3be1f4a728e7f4b48aa16
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370786"
---
# <a name="debugging-a-driver"></a>ドライバーのデバッグ

通常、カーネル モード ドライバーのデバッグには、2 台のコンピューターが必要です。 デバッガーは*ホスト コンピューター*上で実行され、デバッグ対象のコードは*ターゲット コンピューター*上で実行されます。 ターゲット コンピューターは*テスト コンピューター*とも呼ばれます。 ユーザー モード ドライバーは、ホスト コンピューター上でも、別のターゲット コンピューター上でもデバッグできます。 ターゲット コンピューター上で実行されているドライバーをデバッグする前に、ターゲット コンピューターをデバッグ用に構成する必要があります。

ターゲット コンピューターの構成と、デバッグ ケーブルの設定について詳しくは、「[Visual Studio でのカーネル モード デバッグの設定](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-kernel-mode-debugging-in-visual-studio)」と「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」をご覧ください。

Microsoft Visual Studio を使ってドライバーをデバッグする方法について詳しくは、「[Visual Studio を使ったデバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugging-using-visual-studio)」をご覧ください。

Visual Studio を使ってカーネル モード ドライバーをデバッグする例については、「[テンプレートを使った KMDF ドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/writing-a-kmdf-driver-based-on-a-template)」をご覧ください。

Debugging Tools for Windows の概要については、「[Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)」をご覧ください。

## <a name="span-idvideo_demonstrationspanspan-idvideo_demonstrationspanspan-idvideo_demonstrationspanvideo-demonstration"></a><span id="Video_Demonstration"></span><span id="video_demonstration"></span><span id="VIDEO_DEMONSTRATION"></span>ビデオ デモンストレーション


このビデオでは、WinDbg を別に実行するのではなく、Visual Studio で WinDbg デバッグ エンジンを直接使う方法について説明します。

>[!VIDEO https://www.microsoft.com/videoplayer/embed/57464a96-8900-4194-b806-813eb1dd6ac6]





