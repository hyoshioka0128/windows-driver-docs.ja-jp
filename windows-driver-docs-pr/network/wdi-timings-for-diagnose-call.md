---
title: 診断の呼び出しのタイミング
description: デバッグ情報を収集する診断のタイミングの要件は次のとおりです。
ms.assetid: A21687FE-1398-4722-89E3-BFB511AA48E3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19f853cc6890977d16cfdeaf570ae471e7c34b3b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381127"
---
# <a name="timings-for-diagnose-call"></a>診断の呼び出しのタイミング


デバッグ情報を収集する診断のタイミングの要件は次のとおりです。

レベルで**DiagnoseLevelHardwareRegisters**、LE の収集が予想されるデバイスの制御は、診断の呼び出しの出力バッファーに 1 KB を登録します。 これは、通常のリリースの製品の設定です。 デバイス制御レジスタの重要な情報を収集するためのものです。 このような情報を収集する時間の制限は 25 です。

レベルで**DiagnoseLevelFirmwareImageDump**または**DiagnoseLevelDriverStateDump**、デバイス制御レジスタとファームウェアの完全なダンプを収集する、LE が必要です。 時間に余裕がある場合、LE、時間制限の対象のドライバーの状態も収集できます。 診断で収集の制御レジスタは出力バッファー、ダンプのファームウェアとドライバーの状態 %windir% で名前のファイルに保存する必要があります以外\\system32\\ドライバー。 どちらのレベルのすべてのデバッグ情報を収集する時間は、25 秒以内でなければなりません。 これらの診断レベルは、自己ホストのフェーズで使用するためのものです。

## <a name="related-topics"></a>関連トピック


[**eDiagnoseLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ne-dot11wdi-ediagnoselevel)

[*MiniportWdiAdapterHangDiagnose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_adapter_hang_diagnose)

 

 






