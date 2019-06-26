---
title: レガシ オーディオ デバイス メッセージ
description: レガシ オーディオ デバイス メッセージ
ms.assetid: d8b2807b-e72f-4f72-8a83-5700bc0239dc
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49f433e7008f90c9254eae21bab911f11caf5255
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358679"
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

このセクションでは、システムによってインターセプトされ、これまで、デバイス ドライバーに渡されることがなく処理するメッセージのみについて説明します。 詳細については、次を参照してください。 [System-Intercepted デバイス メッセージ](https://docs.microsoft.com/windows-hardware/drivers/audio/system-intercepted-device-messages)します。

このセクションで説明されている各メッセージは、6 つの 1 つ以上で使用するために有効な*xxx*メッセージは上記の関数。

このセクションでは、次のメッセージについて説明します。

[**DRV\_QUERYDEVICEINTERFACE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536363(v=vs.85))

[**DRV\_QUERYDEVICEINTERFACESIZE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536364(v=vs.85))

[**DRV\_QUERYDEVNODE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536365(v=vs.85))

[**DRV\_QUERYMAPPABLE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536366(v=vs.85))

[**DRVM\_MAPPER\_CONSOLEVOICECOM\_GET**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536361(v=vs.85))

[**DRVM\_マッパー\_優先\_取得**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536362(v=vs.85))

 

 





