---
title: x86 ベース マシンの全画面 VDM
description: x86 ベース マシンの全画面 VDM
ms.assetid: 5be4919d-d46f-430f-9d4f-670134379268
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、VGA、x86 ベースのマシンで全画面表示 Vdm
- WDK の VGA ビデオのミニポート、x86 ベースのマシンで全画面表示 Vdm
- x86 ベースのマシン WDK ビデオのミニポートで全画面表示 Vdm
- x86 ベースのマシン WDK VGA と互換性のあるビデオのミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6444c03a427481cbebcbb8042b332fbe6a1771f3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356377"
---
# <a name="full-screen-vdms-in-x86-based-machines"></a>x86 ベース マシンの全画面 VDM


## <span id="ddk_full_screen_vdms_in_x86_based_machines_gg"></span><span id="DDK_FULL_SCREEN_VDMS_IN_X86_BASED_MACHINES_GG"></span>


パフォーマンス上の理由から、ユーザーは、x86 ベースのマシンでは、MS-DOS アプリケーションを全画面表示モードを切り替えると、ディスプレイ ドライバーはアダプターのコントロールを生成します。 VGA、システムまたは VGA と互換性のあるミニポート ドライバー、フックを V86 エミュレーターからアプリケーション発行など、すべての I/O 命令**IN**、 **INSD/REP INSB/INSW**、 **アウト**、および**OUTSD/REP OUTSB/OUTSW**手順については、ビデオの I/O ポートにします。 これらかぎ状の I/O 操作は、VGA と互換性のあるミニポート ドライバーに転送される*SvgaHwIoPortXxx*関数。

ただし、パフォーマンスを向上させる、ミニポート ドライバー呼び出せる[ **VideoPortSetTrappedEmulatorPorts** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportsettrappedemulatorports)へのアクセス、アプリケーションを直接いくつかの I/O ポートを許可します。 ミニポート ドライバーでは、他の I/O ポートをフックは引き続きその*SvgaHwIoPortXxx*をこれらのポートをアプリケーションが発行した命令ストリームを検証します。

全画面表示アプリケーションが、マシンが応答を停止する命令のシーケンスを発行しないように、 *SvgaHwIoPortXxx*関数は、アダプターのレジスタのドライバーにより決定されたセットにアプリケーションの命令ストリームを監視します。 ミニポート ドライバーには、完全に安全では I/O ポートにのみ直接アクセスが有効にする必要があります。 たとえば、sequencer およびその他の出力の登録用のポートする必要があります常に V86 エミュレーターでフックし、ミニポート ドライバーが提供するトラップ*SvgaHwIoPortXxx*検証のための関数。

I/O に直接アクセスするポート (名前は、x86 の I/O のアクセス許可のマップ) IOPM によって判断される VGA と互換性のあるミニポート ドライバーを呼び出すことによって設定する**VideoPortSetTrappedEmulatorPorts**します。 ポート、アプリケーションによって直接アクセスするためにリリースされた、またはに retrapped ミニポート ドライバーがアクセスの範囲、I/O を記述するのには、この関数を呼び出すことによって、IOPM を調整できますに注意してください、 *SvgaHwIoPortXxx*関数。 現在 IOPM を決定するポートは、アプリケーションから直接アクセスできると V86 エミュレーターでフックを維持してをトラップして、 *SvgaHwIoPortXxx*関数を検証します。

既定では、このようなミニポート ドライバーのエミュレーターへのアクセスの範囲の配列を設定するすべての I/O ポートは、対応するトラップされます*SvgaHwIoPortXxx*関数。 ただし、VGA と互換性のあるミニポート ドライバーは、通常を呼び出す**VideoPortSetTrappedEmulatorPorts** IOCTL の受信時に\_ビデオ\_を有効にする\_VDM 要求、のIOPMをリセットする*VDM*これらの I/O ポートの一部に直接アクセスできるようにします。 通常、VGA sequencer レジスタとその他の出力の登録を除くすべてのビデオ アダプター レジスタへの直接アクセスにより、このようなドライバーとドライバー開発者が判断されている SVGA アダプター固有レジスタで常に検証する必要があります、*SvgaHwIoPortXxx*関数。

 

 





