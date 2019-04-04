---
title: レガシ オーディオ デバイス メッセージ
description: レガシ オーディオ デバイス メッセージ
ms.assetid: d8b2807b-e72f-4f72-8a83-5700bc0239dc
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a229b443bbe79263e6d2f65fe87f27f87484662e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580227"
---
# <a name="legacy-audio-device-messages"></a>レガシ オーディオ デバイス メッセージ


## <span id="ddk_legacy_audio_device_messages_ks"></span><span id="DDK_LEGACY_AUDIO_DEVICE_MESSAGES_KS"></span>


次の Windows のマルチ メディア機能は、従来のオーディオ デバイスにメッセージを渡す呼び出し元を提供します。

-   **waveInMessage**

-   **waveOutMessage**

-   **midiInMessage**

-   **midiOutMessage**

-   **mixerMessage**

-   **auxOutMessage**

一部のデバイス メッセージは、デバイス ドライバーによって直接処理され、いくつかは、デバイスに代わって、システムによって処理されます。

このセクションでは、システムによってインターセプトされ、これまで、デバイス ドライバーに渡されることがなく処理するメッセージのみについて説明します。 詳細については、[System-Intercepted デバイス メッセージ](https://msdn.microsoft.com/library/windows/hardware/ff538507)を参照してください。

このセクションで説明されている各メッセージは、6 つの 1 つ以上で使用するために有効な*xxx*メッセージは上記の関数。

このセクションでは、次のメッセージについて説明します。

[**DRV\_QUERYDEVICEINTERFACE**](https://msdn.microsoft.com/library/windows/hardware/ff536363)

[**DRV\_QUERYDEVICEINTERFACESIZE**](https://msdn.microsoft.com/library/windows/hardware/ff536364)

[**DRV\_QUERYDEVNODE**](https://msdn.microsoft.com/library/windows/hardware/ff536365)

[**DRV\_QUERYMAPPABLE**](https://msdn.microsoft.com/library/windows/hardware/ff536366)

[**DRVM\_MAPPER\_CONSOLEVOICECOM\_GET**](https://msdn.microsoft.com/library/windows/hardware/ff536361)

[**DRVM\_マッパー\_優先\_取得**](https://msdn.microsoft.com/library/windows/hardware/ff536362)

 

 





