---
title: X86 ベースのコンピューターの全画面表示の Vdm
description: X86 ベースのコンピューターの全画面表示の Vdm
ms.assetid: 5be4919d-d46f-430f-9d4f-670134379268
keywords:
- ビデオミニポートドライバー (x86 ベースのコンピューターでの WDK Windows 2000、VGA、全画面表示の Vdm)
- VGA WDK ビデオミニポート、x86 ベースのマシンでの全画面表示の Vdm
- x86 ベースのコンピューターでの全画面の Vdm WDK ビデオミニポート
- x86 ベースのコンピューター WDK VGA 互換ビデオミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3832bd85c6e470b10810458518c6d3885691a95
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838939"
---
# <a name="full-screen-vdms-in-x86-based-machines"></a>X86 ベースのコンピューターの全画面表示の Vdm


## <span id="ddk_full_screen_vdms_in_x86_based_machines_gg"></span><span id="DDK_FULL_SCREEN_VDMS_IN_X86_BASED_MACHINES_GG"></span>


パフォーマンス上の理由から、ユーザーが x86 ベースのコンピューターで MS-DOS アプリケーションを全画面表示モードに切り替えると、ディスプレイドライバーによってアダプターが制御されます。 システム VGA または VGA 互換のミニポートドライバーによって、V86 emulator のすべての i/o 命令 (**アプリケーションによって発行さ**れた、**担当者 b/プラグイン、insd**、 **out**、 **rep OUTSB/outsb/outsb**の指示など) がビデオのO ポート。 これらのフックされた i/o 操作は、VGA 互換のミニポートドライバーの*Svガス Hwioportxxx*関数に転送されます。

ただし、パフォーマンスを向上させるために、ミニポートドライバーは[**VideoPortSetTrappedEmulatorPorts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportsettrappedemulatorports)を呼び出すことができます。これにより、アプリケーションから直接、一部の i/o ポートにアクセスできるようになります。 ミニポートドライバーは、他の i/o ポートを*Svガス Hwioportxxx*とフックし続け、アプリケーションによって発行されたこれらのポートへの命令ストリームを検証します。

全画面アプリケーションがコンピューターをハングする可能性のある一連の命令を発行しないようにするために、 *Svガス Hwioportxxx*関数は、ドライバーによって決定されたアダプターレジスタのセットをアプリケーション命令ストリームで監視します。 ミニポートドライバーは、完全に安全な i/o ポートに対してのみ、直接アクセスを有効にする必要があります。 たとえば、sequencer のポートとその他の出力レジスタは、常に V86 emulator によってフックされ、ミニポートドライバーが提供する*Svガス Hwioportxxx*関数にトラップされる必要があります。

アプリケーションの i/o ポートへの直接アクセスは、 **VideoPortSetTrappedEmulatorPorts**を呼び出すことによって、VGA と互換性のあるミニポートドライバーによって設定される IOPM (x86 i/o アクセス許可マップの名前が付いています) によって決まります。 ミニポートドライバーでは、この関数を呼び出すことによって IOPM を調整できます。これは、アプリケーションまたは retrapped が*Sv Hwioportxxx*関数に直接アクセスするために解放された i/o ポートを説明するアクセス範囲を持っています。 現在の IOPM は、アプリケーションから直接アクセスできるポートを決定し、V86 emulator によってフックされたままで、検証のために*Svガス Hwioportxxx*関数にトラップします。

既定では、このようなミニポートドライバーのエミュレーターアクセス範囲配列に設定されているすべての i/o ポートは、対応する*Svare Hwioportxxx*関数にトラップされます。 ただし、通常、VGA と互換性のあるミニポートドライバーは、IOCTL\_ビデオの受信時に**VideoPortSetTrappedEmulatorPorts**を呼び出し\_、VDM の IOPM をリセットし*て、これら*の i/o の一部に直接アクセスできるように\_VDM の要求を有効にします。シリアル. 通常、このようなドライバーを使用すると、VGA sequencer レジスタとその他の出力レジスタを除くすべてのビデオアダプターレジスタに直接アクセスでき、ドライバーライターによって決定されたすべての SVGA アダプター固有のレジスタに対して常に検証する必要があります。*Svガス Hwioportxxx*関数。

 

 





