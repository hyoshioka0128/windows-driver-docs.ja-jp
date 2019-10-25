---
title: USB オーディオ クラス システム ドライバー (Usbaudio.sys)
description: USB オーディオクラスシステムドライバー (Usbaudio .sys) は、オーディオデバイスのユニバーサルシリアルバス (USB) デバイスクラス定義に準拠するオーディオデバイスのドライバーサポートを提供する AVStream ミニドライバーです。
ms.assetid: 7ECE8006-3181-451C-B047-A3D767A7B98A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b5a0e8cc4e5088f88fde230e17d4ebf95423559
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830013"
---
# <a name="usb-audio-class-system-driver-usbaudiosys"></a>USB オーディオ クラス システム ドライバー (Usbaudio.sys)


USB オーディオクラスシステムドライバー (Usbaudio .sys) は、オーディオデバイスのユニバーサルシリアルバス (USB) デバイスクラス定義に準拠するオーディオデバイスのドライバーサポートを提供する AVStream ミニドライバーです。

## <span id="usbaudio_class_system_driver"></span><span id="USBAUDIO_CLASS_SYSTEM_DRIVER"></span>


オーディオデバイス仕様の USB デバイスクラス定義 (リリース 1.0) については、 [Usb 実装者フォーラム](https://go.microsoft.com/fwlink/p/?linkid=8780)の web サイトを参照してください。 Usbaudio は、USB オーディオ仕様で説明されている機能のサブセットをサポートしています。 Usbaudio に加えて、Windows Driver Model (WDM) には他にもカーネルモードのオーディオコンポーネントがいくつかあります。 詳細については、「[カーネルモード WDM オーディオコンポーネント](kernel-mode-wdm-audio-components.md)」を参照してください。

Windows 98 の Usbaudio では、スピーカーやマイクなどの USB デバイスのサポートが導入されました。 Windows Me では、MIDI デバイスのサポートが追加されました。

オーディオデバイスがデバイスの列挙中に USB オーディオに準拠していると識別すると、システムは USBAudio ドライバーを自動的に読み込み、デバイスをドライブにプラグアンドプレイします。 USBAudio は、専用のアダプタードライバーを使用せずに、デバイスを直接ドライブにします。 つまり、USB オーディオ仕様に準拠しているデバイスには、専用のアダプタードライバーは必要ありません。

ハードウェアベンダーは、独自のアダプタードライバーを記述する代わりに、USB オーディオデバイスで USBAudio ドライバーを使用することをお勧めします。

Windows 98 では、USBAudio ドライバーは次の機能をサポートしています。

-   すべての型 I 形式 (8 ビットの符号付き PCM を除く)

-   AC-3 Type II 形式

-   同期とアダプティブの同期の種類

-   マルチチャネルデバイス

ただし、Windows 98 の USBAudio では、次の機能がサポートされていません。

-   8ビットの符号付き PCM 形式

-   MPEG Type II 形式

-   種類 III 形式

-   USB MIDI

-   [**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible) wave 形式 (usbaudio では、代わりに24ビットデータに対して\_PCM\_フォーマットを使用します)。

Windows 98 Second Edition (SE)、Windows Me、および Windows 2000 以降では、USBAudio は Windows 98 と同じ機能をすべてサポートしています。ただし、1つの例外として、USBAudio は WAVEFORMATEXTENSIBLE をサポートしていますが、パックされた WAVE\_形式\_PCM の24ビットをサポートしていません。データ.

Windows Me および Windows XP 以降では、USBAudio は Windows 98 SE および Windows 2000 でサポートされているすべての機能をサポートしています。 さらに、Windows Me と Windows XP では USB MIDI がサポートされていますが、USB MIDI 要素はサポートされていません。

次の図は、USB オーディオデバイスのドライバー階層を示しています。 図に示されているすべてのドライバーコンポーネントは、オペレーティングシステムと共に Microsoft によって提供されます。

![usb オーディオデバイスのドライバー階層を示す図](images/usbaudio.png)

図のドライバーコンポーネントの詳細については、次のセクションを参照してください。

[AVStream の概要](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-overview)

[システム提供の USB ドライバー](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

 

 




