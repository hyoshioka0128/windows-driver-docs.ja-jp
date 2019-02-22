---
title: USB オーディオ クラス システム ドライバー (Usbaudio.sys)
description: USB オーディオ クラスのシステム ドライバー (Usbaudio.sys) では、ユニバーサル シリアル バス (USB) デバイス クラス定義に準拠しているオーディオ デバイス、オーディオ デバイスのドライバーのサポートを提供する AVStream ミニドライバーです。
ms.assetid: 7ECE8006-3181-451C-B047-A3D767A7B98A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 423c229b5b0da49df7a3ab9f5a8c948fff12d88c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550575"
---
# <a name="usb-audio-class-system-driver-usbaudiosys"></a>USB オーディオ クラス システム ドライバー (Usbaudio.sys)


USB オーディオ クラスのシステム ドライバー (Usbaudio.sys) では、ユニバーサル シリアル バス (USB) デバイス クラス定義に準拠しているオーディオ デバイス、オーディオ デバイスのドライバーのサポートを提供する AVStream ミニドライバーです。

## <span id="usbaudio_class_system_driver"></span><span id="USBAUDIO_CLASS_SYSTEM_DRIVER"></span>


オーディオ デバイス仕様 (リリース 1.0) の USB デバイス クラス定義は、 [USB Implementers Forum](https://go.microsoft.com/fwlink/p/?linkid=8780) web サイト。 Usbaudio.sys では、USB オーディオ仕様で説明されている機能のサブセットをサポートしています。 Usbaudio.sys、に加えていくつかその他のカーネル モード オーディオ コンポーネントが Windows Driver Model (WDM) で。 詳細については、次を参照してください。[カーネル モード WDM オーディオ コンポーネント](kernel-mode-wdm-audio-components.md)します。

Windows 98 Usbaudio.sys のスピーカーおよびマイクなどの USB デバイスのサポートが導入されました。 Windows me で MIDI デバイスのサポートが追加されました

オーディオ デバイスが識別されるプラグ アンド プレイ デバイスの列挙中に USB オーディオ対応として、ときに、システムは自動的にデバイスのドライブに USBAudio ドライバーを読み込みます。 USBAudio は、デバイスを直接、独自のアダプターのドライバーの助けなしドライブします。 これは、USB オーディオ仕様に準拠しているデバイスには独自のアダプター ドライバーが必要ないことを意味します。

ハードウェア ベンダーが、独自のアダプターのドライバーを記述する代わりに、USB オーディオ デバイスに対する USBAudio ドライバーを使用することをお勧めします。

Windows 98 では、USBAudio ドライバーには、次の機能がサポートされています。

-   すべて (8 ビット符号付き PCM) を除く形式タイプ I

-   Ac-3 Type II 形式

-   同期およびアダプティブの同期型

-   マルチ デバイス

ただし、Windows 98 で USBAudio をサポートしません。

-   8 ビット符号付きの PCM の形式

-   MPEG Type II 形式

-   III 形式の種類

-   USB MIDI

-   [**WAVEFORMATEXTENSIBLE** ](https://msdn.microsoft.com/library/windows/hardware/ff538802) wave 形式 (USBAudio パックされた波を使用して\_形式\_PCM 24 ビットのデータの代わりにします)。

Windows 98 秒 Edition (SE) Windows Me、および Windows 2000 以降で USBAudio サポートされるすべてが同じ機能として Windows 98 では、1 つの例外。USBAudio WAVEFORMATEXTENSIBLE をサポートしていますが、パックされた波をサポートしていません\_形式\_24 ビットのデータの PCM。

Windows XP と Windows Me で USBAudio が後で、Windows 98 SE、Windows 2000 ではサポートされているすべての機能をサポートしています。 さらに、Windows XP と Windows Me、USB MIDI のサポートは、USB MIDI 要素をサポートしていません。

次の図は、USB オーディオ デバイスのドライバーの階層を示します。 すべての図に示すようにドライバー コンポーネントは、オペレーティング システムと Microsoft によって提供されます。

![usb オーディオ デバイスのドライバーの階層を示す図](images/usbaudio.png)

図に、ドライバー コンポーネントに関する詳細については、次のセクションを参照してください。

[AVStream の概要](https://msdn.microsoft.com/library/windows/hardware/ff554240)

[システム提供の USB ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff538853)

 

 




