---
title: 診断の呼び出しのタイミング
description: デバッグ情報を収集する診断のタイミングの要件は次のとおりです。
ms.assetid: A21687FE-1398-4722-89E3-BFB511AA48E3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45cb96f597367a22feb673b10e4843e8e9adbd70
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356858"
---
# <a name="timings-for-diagnose-call"></a>診断の呼び出しのタイミング


デバッグ情報を収集する診断のタイミングの要件は次のとおりです。

レベルで**DiagnoseLevelHardwareRegisters**、LE の収集が予想されるデバイスの制御は、診断の呼び出しの出力バッファーに 1 KB を登録します。 これは、通常のリリースの製品の設定です。 デバイス制御レジスタの重要な情報を収集するためのものです。 このような情報を収集する時間の制限は 25 です。

レベルで**DiagnoseLevelFirmwareImageDump**または**DiagnoseLevelDriverStateDump**、デバイス制御レジスタとファームウェアの完全なダンプを収集する、LE が必要です。 時間に余裕がある場合、LE、時間制限の対象のドライバーの状態も収集できます。 診断で収集の制御レジスタは出力バッファー、ダンプのファームウェアとドライバーの状態 %windir% で名前のファイルに保存する必要があります以外\\system32\\ドライバー。 どちらのレベルのすべてのデバッグ情報を収集する時間は、25 秒以内でなければなりません。 これらの診断レベルは、自己ホストのフェーズで使用するためのものです。

## <a name="related-topics"></a>関連トピック


[**eDiagnoseLevel**](https://msdn.microsoft.com/library/windows/hardware/mt297626)

[*MiniportWdiAdapterHangDiagnose*](https://msdn.microsoft.com/library/windows/hardware/mt297558)

 

 






