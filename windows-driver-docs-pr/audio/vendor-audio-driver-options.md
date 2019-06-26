---
title: ベンダーのオーディオ ドライバー オプション
description: ベンダーのオーディオ ドライバー オプション
ms.assetid: 4306c027-28ae-4299-83c0-29d892bf64ca
keywords:
- WDM オーディオ ドライバー WDK、ベンダーのオプション
- オーディオ ドライバー WDK、ベンダーのオプション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56043e570d6c66a03e8eaf054de26c1588e6f914
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354131"
---
# <a name="vendor-audio-driver-options"></a>ベンダーのオーディオ ドライバー オプション


## <span id="vendor_audio_driver_options"></span><span id="VENDOR_AUDIO_DRIVER_OPTIONS"></span>


オーディオ デバイスの組み込みのシステムのサポートを利用するには、は、ベンダーが、次のいずれかを使用することをお勧めします。

-   ポート クラス ドライバー (を参照してください[オーディオ ミニポート ドライバー](audio-miniport-drivers.md)) ISA または PCI アダプター カードの

-   USB オーディオ クラス ドライバー (を参照してください[USBAudio クラスのシステム ドライバー](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)) USB オーディオ デバイス

-   カスタムの IEEE 1394 デバイス ドライバー (を参照してください[AVCAudio クラスのシステム ドライバー](kernel-mode-wdm-audio-components.md#avcaudio_class_system_driver))、IEEE 1394 オーディオ デバイスの

ただし、これらのオプションが十分でない場合、ベンダーは、次のいずれかのデータを実装できます。

-   独自の KS フィルター (を参照してください[KS フィルター](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-filters))

-   実装、およびほとんどの ISA、PCI、および USB デバイスに不要なは困難ですが、Microsoft は独自の KS フィルターを勧めしません。

-   Stream クラス ミニドライバー (を参照してください[ストリーミング ミニドライバー](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2))

-   オーディオおよびビデオを統合するデバイスの適切な場合がありますを実装することは困難ですので、Microsoft は、独自のストリーム クラス ミニドライバーを勧めしません。

オーディオ デバイスのドライバーのサポートを提供する使用可能なオプションの詳細については、次を参照してください。 [WDM オーディオ ドライバーの概要](getting-started-with-wdm-audio-drivers.md)します。

 

 




