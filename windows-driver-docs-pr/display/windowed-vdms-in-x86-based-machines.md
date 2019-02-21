---
title: X86 ベースのマシンでのウィンドウの Vdm
description: X86 ベースのマシンでのウィンドウの Vdm
ms.assetid: 01250cef-1ddb-4b32-a155-0170e1e4517a
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、VGA、x86 ベースのマシンでのウィンドウの Vdm
- WDK の VGA ビデオのミニポート、x86 ベースのマシンでのウィンドウの Vdm
- x86 ベースのマシン WDK ビデオのミニポートでウィンドウ Vdm
- x86 ベースのマシン WDK VGA と互換性のあるビデオのミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49eaf87deb795ba00cc6052d2e99169cb1a19998
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550556"
---
# <a name="windowed-vdms-in-x86-based-machines"></a>X86 ベースのマシンでのウィンドウの Vdm


## <span id="ddk_windowed_vdms_in_x86_based_machines_gg"></span><span id="DDK_WINDOWED_VDMS_IN_X86_BASED_MACHINES_GG"></span>


各 MS-DOS アプリケーションは、Windows として実行*VDM*をさらに、保護されたサブシステムの Win32 マネージャーのコンソール アプリケーションとして実行します。

NT ベースのオペレーティング システム プラットフォームでカーネル モード コンポーネントと呼ばれる、 *V86 エミュレーター* MS-DOS アプリケーションによって発行された I/O 命令をトラップします。 ビデオ アダプターのポートにアクセスするには、その試行がトラップされ、システム提供のビデオに反映されますウィンドウ内でこのようなアプリケーションを実行している限り*VDD*アダプタでは、アプリケーションの動作をエミュレートします。

つまり、VDM のウィンドウで実行中にディスプレイ ドライバーは、ビデオ アダプターのコントロールを保持します。

 

 





