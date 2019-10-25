---
title: 診断呼び出しのタイミング
description: デバッグ情報を収集するための診断のタイミング要件は次のとおりです。
ms.assetid: A21687FE-1398-4722-89E3-BFB511AA48E3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e185dbe86ef1d335a0ba1aa69d456c3260466a30
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842890"
---
# <a name="timings-for-diagnose-call"></a>診断呼び出しのタイミング


デバッグ情報を収集するための診断のタイミング要件は次のとおりです。

**DiagnoseLevelHardwareRegisters**のレベルでは、LE は、診断呼び出しの出力バッファーに 1 kb を超えるデバイスコントロールレジスタを収集することが想定されています。 これは、通常のリリース製品の設定です。 これは、デバイスコントロールレジスタの重要な情報を収集することを目的としています。 このような情報を収集するための制限時間は、25ms です。

**DiagnoseLevelFirmwareImageDump**または**DiagnoseLevelDriverStateDump**のレベルでは、LE はデバイスコントロールレジスタとファームウェアの完全ダンプを収集することが想定されています。 時間が許容される場合、LE は、制限時間に従ってドライバーの状態を収集することもできます。 診断出力バッファーに収集されたコントロールレジスタを除き、ファームウェアダンプとドライバーの状態は、% windir%\\system32\\ドライバーで選択した名前のファイルに保存する必要があります。 いずれかのレベルですべてのデバッグ情報を収集する時間は、25秒以内にする必要があります。 これらの診断レベルは、自己ホストフェーズで使用することを意図しています。

## <a name="related-topics"></a>関連トピック


[**eDiagnoseLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ne-dot11wdi-ediagnoselevel)

[*MiniportWdiAdapterHangDiagnose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_adapter_hang_diagnose)

 

 






