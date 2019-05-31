---
title: サンプル周波数に対するハードウェアの制約
description: サンプル周波数に対するハードウェアの制約
ms.assetid: e0041fd9-073c-4779-a3cf-6d0527ba847b
keywords:
- サンプル周波数制約 WDK オーディオ
- 制約のサンプル周波数 WDK オーディオ
- ハードウェアの制約の WDK オーディオ
- 頻度の制約の WDK オーディオ
- 交差部分のデータ ハンドラー WDK オーディオ、サンプル周波数制約
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45e6c7916fb3d4332454f252462cf68d2e713e3f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333610"
---
# <a name="hardware-constraints-on-sample-frequency"></a>サンプル周波数に対するハードウェアの制約


## <span id="hardware_constraints_on_sample_frequency"></span><span id="HARDWARE_CONSTRAINTS_ON_SAMPLE_FREQUENCY"></span>


一部のオーディオ デバイスでは、アダプターのフィルターのシンクの暗証番号 (pin) のサンプル周波数がデジタル出力ポートまたはマイクからの入力ストリームの頻度と一致している必要があります。 たとえば、サウンド Blaster 16 と互換性のあるハードウェアでは、通常、1 つ crystal、同じクロック速度で実行する、入力と出力ストリームに制限があります。 そのさまざまなオンボードのオーディオ ストリームは、複数のクロック速度をサポートできるアダプターは、いくつかの小さな数を別のクロック速度の数を制限するまだ必要があります。

これらの理由から、アダプターのドライバーは、サンプル周波数のオンボードの別のストリームの一致するように 1 つのオンボード ストリームを制限する必要があります。 サウンド Blaster の 16 と互換性のあるアダプターからアダプターのシンクの暗証番号 (pin) のサンプル周波数が出力されるラッチのクロック速度を一致が必要などの Dac。

以前は、KMixer で説明したようでは、Windows Server 2003、Windows XP、Windows 2000、および Windows システム ミキサーをサイトに問題は 98/。 KMixer のソースの暗証番号 (pin) がアダプターのシンクのピンに接続しているときに KMixer は、アダプターを呼び出す必要があります**SetFormat**メソッド (たとえばを参照してください[ **IMiniportWavePciStream::SetFormat** ](https://msdn.microsoft.com/library/windows/hardware/ff536732))その入力のオーディオ ストリームの最も高い頻度のサンプルと一致する接続のサンプル周波数を調整します。 場合は、アダプターは、頻度を変更することはおそらく--オンボード他のストリームのクロック速度に制限があるため、停止する可能性が、 **SetFormat**呼び出します。 詳細を KMixer が応答するこの例では、 **SetFormat**呼び出しが成功するまで、連続して低いサンプル周波数を使用した呼び出し。 KMixer 削減サンプル周波数がもやや後に、サンプル ダウン頻度の高い、入力ストリームそれに応じて。

 

 




