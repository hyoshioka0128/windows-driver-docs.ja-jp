---
title: バグチェック 0x119 VIDEO_SCHEDULER_INTERNAL_ERROR
description: VIDEO_SCHEDULER_INTERNAL_ERROR のバグチェックの値は0x00000119 です。 これは、ビデオスケジューラが致命的な違反を検出したことを示します。
ms.assetid: dfffdd70-c519-4e39-a604-a0ba2217093b
keywords:
- バグチェック 0x119 VIDEO_SCHEDULER_INTERNAL_ERROR
- VIDEO_SCHEDULER_INTERNAL_ERROR
ms.date: 02/07/2020
topic_type:
- apiref
api_name:
- VIDEO_SCHEDULER_INTERNAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d3432d07a66d36e5cd6c01552924e5b9b2cea37d
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534663"
---
# <a name="bug-check-0x119-video_scheduler_internal_error"></a>バグチェック 0x119: ビデオ \_ スケジューラの \_ 内部 \_ エラー

ビデオ \_ スケジューラの \_ 内部エラーのバグチェックには、 \_ 値0x00000119 が含まれています。 これは、ビデオスケジューラが致命的な違反を検出したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

## <a name="video_scheduler_internal_error-parameters"></a>ビデオ \_ スケジューラの \_ 内部 \_ エラーパラメーター

パラメーター1は目的の唯一のパラメーターであり、正確な違反を識別します。

| パラメーター 1 | エラーの原因                                       |
|-----------|--------------------------------------------------------|
|0x1|ドライバーが無効なフェンス ID を報告しました。 |
|0x2| コマンドの送信時にドライバーが失敗しました。|
|0x3|コマンドバッファーにパッチを適用したときにドライバーが失敗しました。 |
|0x4| ドライバーが無効なフリップ機能を報告しました。|
|0x5| ドライバーがシステムまたはページングコマンドを実行できませんでした。|
|0x400| これは、通常、メモリの破損やハードウェアの不具合が原因で発生する内部 OS 状態エラーです。|
|0xE00 | OS は、事前に割り当てられたパケットがパッシブフリップ要求を処理するためにメモリ不足になりました。|
|0x1000| これは、通常、メモリの破損やハードウェアの不具合が原因で発生する内部 OS 状態エラーです。|
|0x10000| これは、通常、メモリの破損やハードウェアの不具合が原因で発生する内部 OS 状態エラーです。|

## <a name="resolution"></a>解像度

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。

! Analyze 出力に示されているエラーモジュールがビデオドライバーの場合は、そのビデオドライバーで更新プログラムがベンダから入手可能かどうかを調査します。

詳細については、次を参照してください。

[コマンドおよび DMA バッファーの処理](https://docs.microsoft.com/windows-hardware/drivers/display/handling-command-and-dma-buffers)

[コマンド バッファーの送信](https://docs.microsoft.com/windows-hardware/drivers/display/submitting-a-command-buffer)

[フェンス識別子の提供](https://docs.microsoft.com/windows-hardware/drivers/display/supplying-fence-identifiers)

[GPU スケジューラ クラス](https://docs.microsoft.com/windows-hardware/drivers/display/gpu-scheduler-class)

[ビデオ メモリの直接の反転](https://docs.microsoft.com/windows-hardware/drivers/display/direct-flip-of-video-memory)