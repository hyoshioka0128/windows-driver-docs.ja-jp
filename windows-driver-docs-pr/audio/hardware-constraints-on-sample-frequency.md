---
title: サンプル周波数に対するハードウェアの制約
description: サンプル周波数に対するハードウェアの制約
ms.assetid: e0041fd9-073c-4779-a3cf-6d0527ba847b
keywords:
- サンプル頻度制約 WDK オーディオ
- サンプル頻度 WDK オーディオを制限する
- ハードウェア制約 WDK オーディオ
- 頻度の制約 WDK オーディオ
- データ交差ハンドラー WDK audio、サンプル頻度制約
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81a1141ee10b40d1b16ac058af9517fb2d4a020e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831223"
---
# <a name="hardware-constraints-on-sample-frequency"></a>サンプル周波数に対するハードウェアの制約


## <span id="hardware_constraints_on_sample_frequency"></span><span id="HARDWARE_CONSTRAINTS_ON_SAMPLE_FREQUENCY"></span>


一部のオーディオデバイスでは、アダプターフィルターのシンク pin のサンプル周波数が、デジタル出力ポートの周波数またはマイクからの入力ストリームと一致している必要があります。 たとえば、Sound Blaster 16 と互換性のあるハードウェアには、通常、1つの crystal があり、入力ストリームと出力ストリームは同じクロックレートで実行されるように制限されています。 さまざまなオンボードオーディオストリームに対して複数のクロックレートをサポートできるアダプターでも、異なるクロックレートの数をいくつかの小さな数値に制限する必要がある場合があります。

このような理由から、アダプタードライバーでは、1つのオンボードストリームでサンプル頻度を制限して、別のオンボードストリームと一致させることが必要になる場合があります。 たとえば、Sound Blaster 16 互換アダプターでは、アダプターのシンク pin のサンプル周波数が、出力 Dac でのラッチのクロックレートと一致している必要があります。

既に説明したように、KMixer は、Windows Server 2003、Windows XP、Windows 2000、および Windows Me/98 のシステムミキサーです。 KMixer のソース pin がアダプターのシンク pin に接続されている場合、KMixer は、アダプターの**setformat**メソッド (たとえば、 [**IMiniportWavePciStream:: setformat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-setformat)を参照) を呼び出して、接続でのサンプル頻度を調整し、入力時のオーディオストリームの最大サンプル周波数。 アダプターが周波数を変更できない場合 (他のオンボードストリームのクロックレートによって制限されている場合など)、 **Setformat**呼び出しが失敗する可能性があります。 この場合、KMixer は、呼び出しが成功するまで、より小さなサンプル周波数でより多くの**Setformat**呼び出しを行うことで応答します。 KMixer が低サンプル頻度で決済されると、それに応じて、より高い頻度の入力ストリームがサンプリングされます。

 

 




