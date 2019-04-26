---
title: VGA 互換ミニポート ドライバーの HwVidStartIO
description: VGA 互換ミニポート ドライバーの HwVidStartIO
ms.assetid: e5a81f87-b220-4497-aed3-8c4d08504340
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、VGA、HwVidStartIO
- WDK の VGA ビデオのミニポート HwVidStartIO
- HwVidStartIO
- VGA-互換性のあるビデオのミニポート ドライバー WDK
- SVGA WDK ビデオのミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c7cf64a18633bbba8aaf664a794a34a3f53d697
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354831"
---
# <a name="vga-compatible-miniport-drivers-hwvidstartio"></a>VGA 互換ミニポート ドライバーの HwVidStartIO


## <span id="ddk_vga_compatible_miniport_driver_s_hwvidstartio_gg"></span><span id="DDK_VGA_COMPATIBLE_MINIPORT_DRIVER_S_HWVIDSTARTIO_GG"></span>


ユーザーの VGA と互換性のあるミニポート ドライバーのウィンドウで、実行中に戻す MS-DOS アプリケーションを全画面表示を切り替えるとき*HwVidStartIO* I/O 制御コード IOCTL\_ビデオ\_保存\_ハードウェア\_状態。 ユーザーがもう一度アプリケーションを全画面表示モードを切り替える場合に、ミニポート ドライバーはアダプターの状態を格納する必要があります。

なお、ミニポート ドライバーの*SvgaHwIoPortXxx*関数がアプリケーションのシーケンスにバッファリングされるが**IN**s や**アウト**」の説明に従って、s [SvgaHwIoPortXxx の指示を検証する](validating-instructions-in-svgahwioportxxx.md)ときに、その*HwVidStartIO*関数は、アダプターの状態を保存します。 このような場合は、ミニポート ドライバーがバッファー内の手順を含め、現在の状態を保存する必要がありますように、 *SvgaHwIoPortXxx*関数が正確に中断された場合、ユーザーの検証操作を再開できます全画面表示モードをアプリケーションに切り替えます。

ミニポート ドライバーでの保存の完了時に操作を自動的に無効にしますの現在の IOPM のポート ドライバー *VDM*秒と、ミニポート ドライバーの*SvgaHwIoPortXxx*関数。 ビデオ ポート ドライバー再度、アプリケーションが全画面表示モードに切り替える場合、IOPM は自動的に復元します。 ミニポート ドライバーの呼び出しも再開*SvgaHwIoPortXxx*関数は、ミニポート ドライバーの呼び出された後*HwVidStartIO* IOCTL で関数を\_ビデオ\_復元\_ハードウェア\_状態要求。

 

 





