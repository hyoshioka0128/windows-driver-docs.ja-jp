---
title: DirectSound のソフトウェア バッファーとハードウェア バッファーを使用した Wave コンテンツのレンダリング
description: DirectSound のソフトウェア バッファーとハードウェア バッファーを使用した Wave コンテンツのレンダリング
ms.assetid: df92dac3-2580-4910-8a55-bd9e9f82eb1f
keywords:
- DirectSound WDK のオーディオ、コンテンツのレンダリング
- wave WDK オーディオのコンテンツのレンダリング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 082c62d647746a0fa4362046473ec40754e10c20
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328714"
---
# <a name="rendering-wave-content-using-directsound-software-and-hardware-buffers"></a>DirectSound のソフトウェア バッファーとハードウェア バッファーを使用した Wave コンテンツのレンダリング


## <span id="ddk_rendering_wave_content_using_directsound_software_and_hardware_buf"></span><span id="DDK_RENDERING_WAVE_CONTENT_USING_DIRECTSOUND_SOFTWARE_AND_HARDWARE_BUF"></span>


次の図は、Microsoft Windows Driver Model (WDM) コンポーネントの構成であり、DirectSound のソフトウェアとハードウェアを表示するためのバッファーを示します。

![directsound ソフトウェアとハードウェアのバッファーを使用してレンダリング wave コンテンツを示す図します。](images/hwbuf.png)

WDM オーディオ コンポーネントの説明については、次を参照してください。

[DirectSound システム コンポーネント](user-mode-wdm-audio-components.md#directsound_system_component)

[SysAudio システム ドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)

[KMixer システム ドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)

[ポート クラスのアダプターのドライバーと PortCls システム ドライバー](kernel-mode-wdm-audio-components.md#port_class_adapter_driver_and_portcls_system_driver)

[USBAudio クラスのシステム ドライバー](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)

 

 




