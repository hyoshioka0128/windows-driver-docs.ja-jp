---
title: デバイスのシステム インターセプト メッセージ
description: デバイスのシステム インターセプト メッセージ
ms.assetid: 5cf1c9a6-e56f-4358-933f-e8aa2ad1b1da
keywords:
- レガシ デバイス WDK オーディオ デバイス メッセージ
- WDM オーディオ拡張 WDK、システム インターセプト デバイス メッセージ
- デバイスのシステム インターセプト メッセージ WDK オーディオ
- メッセージの WDK オーディオ
- 受信済みのデバイス メッセージ WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4623a07cb6a70873934bcfcab66b99e95ca28590
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528349"
---
# <a name="system-intercepted-device-messages"></a>デバイスのシステム インターセプト メッセージ


## <span id="system_intercepted_device_messages"></span><span id="SYSTEM_INTERCEPTED_DEVICE_MESSAGES"></span>


次の Windows マルチ メディア関数は、従来のオーディオ デバイスにメッセージを渡す呼び出し元の方法を提供します。

-   [**waveInMessage**](https://msdn.microsoft.com/library/windows/desktop/dd743846)

-   [**waveOutMessage**](https://msdn.microsoft.com/library/windows/desktop/dd743865)

-   [**midiInMessage**](https://msdn.microsoft.com/library/windows/desktop/dd798457)

-   [**midiOutMessage**](https://msdn.microsoft.com/library/windows/desktop/dd798475)

-   [**mixerMessage**](https://msdn.microsoft.com/library/windows/desktop/dd757307)

-   [**auxOutMessage**](https://msdn.microsoft.com/library/windows/desktop/dd756716)

一部のデバイス メッセージは、デバイス ドライバーによって直接処理され、いくつかは、デバイスに代わって、システムによって処理されます。

このセクションでは、システムによってインターセプトされ、これまで、デバイス ドライバーに渡されることがなく処理するメッセージのみについて説明します。 システム インターセプト メッセージには、音声通信または一般的なオーディオの使用方法の好みのデバイスを取得できます。 さらに、システム インターセプト メッセージは、特定のデバイスに関する次の情報を提供できます。

-   **デバイスのインターフェイス名**

    デバイス インターフェイス名については、次を参照してください。[デバイス インターフェイスの概要](https://msdn.microsoft.com/library/windows/hardware/ff549460)します。

-   **デバイスのプラグ アンド プレイ devnode 番号**

    Devnode については、次を参照してください。[デバイス ツリー](https://msdn.microsoft.com/library/windows/hardware/ff543194)します。

-   **デバイスを使用して、マッパーによってかどうか**

    マッパーは、システムで使用可能なデバイスのいずれかに、アプリケーションの要件をマッピングすることによって、適切なデバイスを選択します。 マッパーの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

その他の種類のデバイス メッセージについては、Windows SDK のドキュメントを参照してください。

*Xxx*メッセージ関数は、次の構文。

```cpp
DWORD XxxMessage(
<device ID>,
    UINT  uMsg,
    DWORD_PTR  dwParam1,
    DWORD_PTR  dwParam2
    );
```

最初のパラメーターは、デバイスの id です。 [ **AuxOutMessage** ](https://msdn.microsoft.com/library/windows/desktop/dd756716)関数の定義が期待どおりに、このパラメーターの型 UINT を指定します。 ただしの場合[ **waveInMessage**](https://msdn.microsoft.com/library/windows/desktop/dd743846)、 [ **waveOutMessage**](https://msdn.microsoft.com/library/windows/desktop/dd743865)、 [ **midiInMessage**](https://msdn.microsoft.com/library/windows/desktop/dd798457)、 [ **midiOutMessage**](https://msdn.microsoft.com/library/windows/desktop/dd798475)、または[ **mixerMessage**](https://msdn.microsoft.com/library/windows/desktop/dd757307)、呼び出し元が型を処理するためにデバイス ID をキャストする必要がありますHWAVEIN、HWAVEOUT、HMIDIIN、HMIDIOUT、または HMIXER、それぞれします。 注こと、呼び出し元がこのパラメーターのデバイス ID ではなく、有効なハンドルを提供している場合、関数は失敗し、エラー コードを MMSYSERR 返します\_NOSUPPORT します。

*UMsg*パラメーターがメッセージの値を指定します (たとえば、 [ **DRV\_QUERYDEVICEINTERFACE**](https://msdn.microsoft.com/library/windows/hardware/ff536363))。 ドライバー固有のメッセージの一覧は、ヘッダー ファイル Mmddk.h を参照してください。

パラメーターの意味*dwParam1*と*dwParam2*メッセージに依存します。 たとえば、特定のメッセージが必要がありますを*dwParam1* ULONG の値を指定、呼び出し元はこの値を DWORD 型をキャストする必要があります\_PTR 関数の定義を満たすためにします。

返します MMERR\_NOERROR 呼び出しが成功すると、そうでない場合はエラー状態コード。

詳細については、 *Xxx*メッセージ関数を Windows SDK のマニュアルを参照してください。

ヘッダー ファイル Mmddk.h では、次のシステム インターセプト デバイス メッセージを定義します。

[**DRV\_QUERYDEVICEINTERFACE**](https://msdn.microsoft.com/library/windows/hardware/ff536363)

詳細については、次を参照してください。[デバイス インターフェイスの名前を取得する](obtaining-a-device-interface-name.md)します。

[**DRV\_QUERYDEVICEINTERFACESIZE**](https://msdn.microsoft.com/library/windows/hardware/ff536364)

詳細については、次を参照してください。**デバイス インターフェイスの名前を取得する**します。

[**DRV\_QUERYDEVNODE**](https://msdn.microsoft.com/library/windows/hardware/ff536365)

デバイスの devnode 数を照会します。

[**DRV\_QUERYMAPPABLE**](https://msdn.microsoft.com/library/windows/hardware/ff536366)

デバイスが、マッパーで使用できるかどうかを照会します。

[**DRVM\_MAPPER\_CONSOLEVOICECOM\_GET**](https://msdn.microsoft.com/library/windows/hardware/ff536361)

詳細については、次を参照してください。[音声通信デバイス ID の優先](preferred-voice-communications-device-id.md)します。

[**DRVM\_マッパー\_優先\_取得**](https://msdn.microsoft.com/library/windows/hardware/ff536362)

詳細については、次を参照してください。[優先デバイス ID にアクセスする](accessing-the-preferred-device-id.md)します。

 

 




