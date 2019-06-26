---
title: カスタム オーディオ ドライバーの種類のデシジョン ツリー
description: カスタム オーディオ ドライバーの種類のデシジョン ツリー
ms.assetid: 7b055baa-1843-4e31-a98e-48b05de94e70
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9302fd8481b5ff7060dea4523a6779353ad39fee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359110"
---
# <a name="custom-audio-driver-type-decision-tree"></a>カスタム オーディオ ドライバーの種類のデシジョン ツリー


このデシジョン ツリーを使用して、手順 3 の[WDM オーディオ ドライバーの開発のためのロードマップ](roadmap-for-developing-wdm-audio-drivers.md)します。 ツリーを使用して、詳細については、オーディオ ドライバーの種類を決定するのに役立ちます。 システム指定のポートのクラス ドライバー (PortCls) では、ほとんどの基本的な機能を実装するポートのドライバーのセットを提供します。 これらのポート ドライバーはドライバー開発者向けの開発プロセスを簡略化します。 高精細 (HD) オーディオおよび AC97 ドライバーは通常、基づいて PortCls クラス ドライバーを USB と 1394 ドライバーには、通常 AVStream クラスに基づきますが、します。

![オーディオ ドライバーの種類の選択のデシジョン ツリーの図](images/roadmap-uaacomp.png)

オーディオ デバイスは、ユニバーサル オーディオ アーキテクチャに基づいて (UAA) 標準場合、UAA 互換性があります。 UAA と互換性のあるオーディオ デバイスがシステム提供の UAA クラス ドライバーを使用でき、カスタム ドライバーでは、必要はありませんが、独自に提供することができます[Windows オーディオ処理オブジェクト](windows-audio-processing-objects.md)します。

オーディオ デバイスですがない場合 UAA と互換性のあるまたは UAA と互換性のあるカスタマイズされた機能を実装する場合、バス マスター DMA サポートでのドライバーを開発するかどうかを決定する必要があります。 バス マスター DMA サポートを提供する場合は、たとえば、PortCls ベースのオーディオ ドライバーを開発する必要があります。

カスタム オーディオ ドライバーを開発する方法とポートのドライバーを選択する方法については、次のトピックを参照してください。

<span id="Custom_Audio_Drivers"></span><span id="custom_audio_drivers"></span><span id="CUSTOM_AUDIO_DRIVERS"></span>[カスタム オーディオ ドライバー](custom-audio-drivers.md)  
PortCls と AVStream のオーディオ ドライバーの概要を説明し、長所と短所の各種類について説明します。

<span id="AVStream_Overview"></span><span id="avstream_overview"></span><span id="AVSTREAM_OVERVIEW"></span>[AVStream の概要](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-overview)  
AVStream ベースのドライバーのアーキテクチャの概要を提供し、この種類のドライバーが最適な選択肢をケースを強調表示します。

について、オーディオ ドライバーを使用するデータ形式と、さまざまな形式をサポートする必要もあります。 データ形式と範囲の詳細については、次を参照してください。[オーディオ データ形式とデータ範囲](audio-data-formats-and-data-ranges.md)します。

オーディオ ドライバーの開発のための手順を完了するを参照してください。 [WDM オーディオ ドライバーの開発のためのロードマップ](roadmap-for-developing-wdm-audio-drivers.md)します。

 

 




