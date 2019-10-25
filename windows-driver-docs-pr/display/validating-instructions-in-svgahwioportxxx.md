---
title: SvgaHwIoPortXxx の指示の検証
description: SvgaHwIoPortXxx の指示の検証
ms.assetid: 70fe2acb-10ff-4182-96a5-78bff0d8f8a0
keywords:
- ビデオミニポートドライバー WDK Windows 2000、VGA、Svガス Hwioportxxx 関数
- VGA WDK ビデオミニポート、Svガス Hwioportxxx 関数
- Svガス Hwioportxxx 関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0307c5cd6b80c19619b4c1a30374e8be619f0689
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825331"
---
# <a name="validating-instructions-in-svgahwioportxxx"></a>SvgaHwIoPortXxx の指示の検証


## <span id="ddk_validating_instructions_in_svgahwioportxxx_gg"></span><span id="DDK_VALIDATING_INSTRUCTIONS_IN_SVGAHWIOPORTXXX_GG"></span>


既に説明したように、 [VGA 互換のミニポートドライバーの HwVidFindAdapter](vga-compatible-miniport-driver-s-hwvidfindadapter.md)では、直接アクセス可能な i/o ポートの IOPM セットには、通常、sequencer レジスタとその他の出力レジスタを除くすべての SVGA レジスタが含まれます。VGA と互換性のあるミニポートドライバーは、 *Svガス Hwioportxxx*関数を使用して引き続き監視します。 Sequencer は、VGA と互換性のあるビデオアダプターにコントロールの内部チップタイミングを登録します。 同期リセット中に、全画面表示の MS-DOS アプリケーションが他のアダプターレジスタに触れると、マシンがハングすることがあります。 同様に、その他の出力レジスタが存在しないクロックを選択するように設定されている場合、マシンはハングする可能性があります。

VGA 互換のミニポートドライバーでは、全画面表示の MS-DOS アプリケーションが、マシンがハングする原因となる命令を発行しないようにする必要があります。 各ミニポートドライバーは、アダプター sequencer レジスタおよびその他の出力レジスタの i/o ポートに対して、アプリケーションによって発行された命令を監視する*Svガス Hwioportxxx*関数を提供する必要があります。 特別な機能を備えたアダプター用の新しい VGA 互換のミニポートドライバーでは、アプリケーションがコンピューターの接続を切断する命令シーケンスを送信する可能性のある i/o ポートも監視して、引き続き検証する必要があります。

アプリケーションが sequencer clock register にアクセスしようとするたびに、 *Svガス Hwioportxxx*関数は、同期リセット中に発生したすべての命令をトラップするために、IOPM を変更する必要があります。 アプリケーションが sequencer に影響を与える命令を送信したり、その他の出力レジスタへの書き込みを試行したりするとすぐに、 *Svガス Hwioportxxx*関数は、 [**VideoPortSetTrappedEmulatorPorts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportsettrappedemulatorports)を呼び出して IOPM を調整し、無効にします。すべてのアダプターレジスタに直接アクセスします。

ミニポートドライバーによって提供される*Svガス Hwioportxxx*関数は、 **EmulatorAccessEntriesContext**領域内の後続の (または、/ **insd**では、または、 **OUTSB/outsb/outsb**/ **OUT** ) 命令の後**に**バッファリングする必要があります。同期リセットが完了するまで、またはアプリケーションがその他の出力レジスタを復元またはリセットするまで、ビデオ\_ポート\_CONFIG\_情報を設定します (「 [VGA 互換のミニポートドライバーの HwVidFindAdapter](vga-compatible-miniport-driver-s-hwvidfindadapter.md)」を参照してください)。"安全な" 時計にします。

次に、ミニポートドライバーは、バッファーされた命令がコンピューターをハングできないことを確認します。 それ以外の場合、ミニポートドライバーはバッファーされた命令を処理する必要があります。通常は、ドライバーによって提供される[*HwVidSynchronizeExecutionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pminiport_synchronize_routine)関数を使用して[**VideoPortSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportsynchronizeexecution)を呼び出します。 それ以外の場合、ミニポートドライバーはバッファーされた命令を破棄する必要があります。

 

 





