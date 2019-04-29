---
title: SvgaHwIoPortXxx の指示の検証
description: SvgaHwIoPortXxx の指示の検証
ms.assetid: 70fe2acb-10ff-4182-96a5-78bff0d8f8a0
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、VGA、SvgaHwIoPortXxx 関数
- WDK の VGA ビデオのミニポート SvgaHwIoPortXxx 関数
- SvgaHwIoPortXxx 関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f71dff7bcd3a1b74c179e7c6f479525d88d60a32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390804"
---
# <a name="validating-instructions-in-svgahwioportxxx"></a>SvgaHwIoPortXxx の指示の検証


## <span id="ddk_validating_instructions_in_svgahwioportxxx_gg"></span><span id="DDK_VALIDATING_INSTRUCTIONS_IN_SVGAHWIOPORTXXX_GG"></span>


説明したように[VGA と互換性のあるミニポート ドライバー HwVidFindAdapter](vga-compatible-miniport-driver-s-hwvidfindadapter.md)IOPM、直接アクセス可能な I/O ポートには通常が含まれています、sequencer レジスタとその他の出力の登録を除くすべての SVGA レジスタには設定、で監視する VGA と互換性のあるミニポート ドライバーが引き続きその*SvgaHwIoPortXxx*関数。 Sequencer は、VGA と互換性のあるビデオ アダプターを内部のチップのタイミングを制御を登録します。 全画面表示の MS-DOS アプリケーションは、同期のリセット中に他のアダプターのレジスタをタッチ、マシンがハングすることができます。 同様に、その他の出力の登録が存在しない時刻を選択する設定されている場合、マシンがハングできます。

VGA と互換性のあるミニポート ドライバーは、MS-DOS アプリケーションを全画面表示が、コンピューターでハングが発生する手順を実行しないようにことを確認する必要があります。 このような各ミニポート ドライバーを指定する必要があります*SvgaHwIoPortXxx*アダプター sequencer レジスタとその他の I/O ポートをアプリケーションが発行した命令を監視する機能が登録を出力します。 特殊な機能を使用するアダプターの新しい各 VGA と互換性のあるミニポート ドライバーもして監視がアプリケーションが、マシンがハングする任意の命令シーケンスを送信がすべての I/O ポートを検証する必要があります。

アプリケーションは、sequencer クロック レジスタへのアクセスを試みるたびに、 *SvgaHwIoPortXxx*関数は、同期のリセット中にで導入されるすべての命令をトラップするために、IOPM を変更する必要があります。 アプリケーションが、sequencer に影響するか、またはその他の出力を書き込もうとする命令を送信するとすぐ、 *SvgaHwIoPortXxx*関数が呼び出すことによって、IOPM を調整する必要があります[ **VideoPortSetTrappedEmulatorPorts** ](https://msdn.microsoft.com/library/windows/hardware/ff570366)アダプターのすべてのレジスタへの直接アクセスを無効にします。

ミニポート ドライバーによって提供される*SvgaHwIoPortXxx*関数はバッファーの後続**IN** (または**INSB/INSW/INSD**) や**アウト**(または**OUTSB/OUTSW/OUTSD**)」の手順に、 **EmulatorAccessEntriesContext**ビデオに設定する領域\_ポート\_CONFIG\_情報 (を参照してください[VGA と互換性のあるミニポート ドライバー HwVidFindAdapter](vga-compatible-miniport-driver-s-hwvidfindadapter.md)) 同期のリセットを完了すると、まで、またはアプリケーションがその他の出力の登録を復元または、「安全」クロックにリセットされます。

次に、ミニポート ドライバーは、バッファー内の手順については、コンピューターでハングすることはできませんのチェックを担当します。 処理されない場合、ミニポート ドライバーがバッファー内の手順では、通常を呼び出して[ **VideoPortSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff570372)ドライバーによって提供されると[ *HwVidSynchronizeExecutionCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff567369)関数。 それ以外の場合、ミニポート ドライバーでは、バッファー内の指示を破棄する必要があります。

 

 





