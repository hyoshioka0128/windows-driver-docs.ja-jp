---
ms.assetid: 2274e848-2a0b-445c-82cd-7bcd9e23078a
title: ドライバーのデバッグ
description: 通常、カーネル モード ドライバーのデバッグには、2 台のコンピューターが必要です。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89c126f5a8429d6cff5d6dc50a314fa3def99d48
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63382348"
---
# <a name="debugging-a-driver"></a>ドライバーのデバッグ

通常、カーネル モード ドライバーのデバッグには、2 台のコンピューターが必要です。 デバッガーは*ホスト コンピューター*上で実行され、デバッグ対象のコードは*ターゲット コンピューター*上で実行されます。 ターゲット コンピューターは*テスト コンピューター*とも呼ばれます。 ユーザー モード ドライバーは、ホスト コンピューター上でも、別のターゲット コンピューター上でもデバッグできます。 ターゲット コンピューター上で実行されているドライバーをデバッグする前に、ターゲット コンピューターをデバッグ用に構成する必要があります。

ターゲット コンピューターの構成と、デバッグ ケーブルの設定について詳しくは、「[Visual Studio でのカーネル モード デバッグの設定](https://msdn.microsoft.com/windows/hardware/hh439376)」と「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 8.1)](https://msdn.microsoft.com/Library/Windows/Hardware/Dn745909)」をご覧ください。

Microsoft Visual Studio を使ってドライバーをデバッグする方法について詳しくは、「[Visual Studio を使ったデバッグ](https://msdn.microsoft.com/Library/Windows/Hardware/Hh406281)」をご覧ください。

Visual Studio を使ってカーネル モード ドライバーをデバッグする例については、「[テンプレートを使った KMDF ドライバーの作成](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439654)」をご覧ください。

Debugging Tools for Windows の概要については、「[Windows デバッグ](https://msdn.microsoft.com/Library/Windows/Hardware/Ff551063)」をご覧ください。

## <a name="span-idvideodemonstrationspanspan-idvideodemonstrationspanspan-idvideodemonstrationspanvideo-demonstration"></a><span id="Video_Demonstration"></span><span id="video_demonstration"></span><span id="VIDEO_DEMONSTRATION"></span>ビデオ デモンストレーション


このビデオでは、WinDbg を別に実行するのではなく、Visual Studio で WinDbg デバッグ エンジンを直接使う方法について説明します。

>[!VIDEO https://www.microsoft.com/videoplayer/embed/57464a96-8900-4194-b806-813eb1dd6ac6]





