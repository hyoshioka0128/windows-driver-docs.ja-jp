---
title: システムでインターセプトされるデバイス メッセージ
description: システムでインターセプトされるデバイス メッセージ
ms.assetid: 5cf1c9a6-e56f-4358-933f-e8aa2ad1b1da
keywords:
- レガシ デバイス WDK オーディオ デバイス メッセージ
- WDM オーディオ拡張 WDK、システム インターセプト デバイス メッセージ
- デバイスのシステム インターセプト メッセージ WDK オーディオ
- メッセージの WDK オーディオ
- 受信済みのデバイス メッセージ WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d132c3c25f07419b71be182b9754b9aa9041f276
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364813"
---
# <a name="system-intercepted-device-messages"></a>システムでインターセプトされるデバイス メッセージ


## <span id="system_intercepted_device_messages"></span><span id="SYSTEM_INTERCEPTED_DEVICE_MESSAGES"></span>


次の Windows マルチ メディア関数は、従来のオーディオ デバイスにメッセージを渡す呼び出し元の方法を提供します。

-   [**waveInMessage**](https://docs.microsoft.com/previous-versions/dd743846(v=vs.85))

-   [**waveOutMessage**](https://docs.microsoft.com/previous-versions/dd743865(v=vs.85))

-   [**midiInMessage**](https://docs.microsoft.com/previous-versions/dd798457(v=vs.85))

-   [**midiOutMessage**](https://docs.microsoft.com/previous-versions/dd798475(v=vs.85))

-   [**mixerMessage**](https://docs.microsoft.com/previous-versions/dd757307(v=vs.85))

-   [**auxOutMessage**](https://docs.microsoft.com/previous-versions/dd756716(v=vs.85))

一部のデバイス メッセージは、デバイス ドライバーによって直接処理され、いくつかは、デバイスに代わって、システムによって処理されます。

このセクションでは、システムによってインターセプトされ、これまで、デバイス ドライバーに渡されることがなく処理するメッセージのみについて説明します。 システム インターセプト メッセージには、音声通信または一般的なオーディオの使用方法の好みのデバイスを取得できます。 さらに、システム インターセプト メッセージは、特定のデバイスに関する次の情報を提供できます。

-   **デバイスのインターフェイス名**

    デバイス インターフェイス名については、次を参照してください。[デバイス インターフェイスの概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-interface-classes)します。

-   **デバイスのプラグ アンド プレイ devnode 番号**

    Devnode については、次を参照してください。[デバイス ツリー](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)します。

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

最初のパラメーターは、デバイスの id です。 [ **AuxOutMessage** ](https://docs.microsoft.com/previous-versions/dd756716(v=vs.85))関数の定義が期待どおりに、このパラメーターの型 UINT を指定します。 ただしの場合[ **waveInMessage**](https://docs.microsoft.com/previous-versions/dd743846(v=vs.85))、 [ **waveOutMessage**](https://docs.microsoft.com/previous-versions/dd743865(v=vs.85))、 [ **midiInMessage**](https://docs.microsoft.com/previous-versions/dd798457(v=vs.85))、 [ **midiOutMessage**](https://docs.microsoft.com/previous-versions/dd798475(v=vs.85))、または[ **mixerMessage**](https://docs.microsoft.com/previous-versions/dd757307(v=vs.85))、呼び出し元が型を処理するためにデバイス ID をキャストする必要がありますHWAVEIN、HWAVEOUT、HMIDIIN、HMIDIOUT、または HMIXER、それぞれします。 注こと、呼び出し元がこのパラメーターのデバイス ID ではなく、有効なハンドルを提供している場合、関数は失敗し、エラー コードを MMSYSERR 返します\_NOSUPPORT します。

*UMsg*パラメーターがメッセージの値を指定します (たとえば、 [ **DRV\_QUERYDEVICEINTERFACE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536363(v=vs.85)))。 ドライバー固有のメッセージの一覧は、ヘッダー ファイル Mmddk.h を参照してください。

パラメーターの意味*dwParam1*と*dwParam2*メッセージに依存します。 たとえば、特定のメッセージが必要がありますを*dwParam1* ULONG の値を指定、呼び出し元はこの値を DWORD 型をキャストする必要があります\_PTR 関数の定義を満たすためにします。

返します MMERR\_NOERROR 呼び出しが成功すると、そうでない場合はエラー状態コード。

詳細については、 *Xxx*メッセージ関数を Windows SDK のマニュアルを参照してください。

ヘッダー ファイル Mmddk.h では、次のシステム インターセプト デバイス メッセージを定義します。

[**DRV\_QUERYDEVICEINTERFACE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536363(v=vs.85))

詳細については、次を参照してください。[デバイス インターフェイスの名前を取得する](obtaining-a-device-interface-name.md)します。

[**DRV\_QUERYDEVICEINTERFACESIZE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536364(v=vs.85))

詳細については、次を参照してください。**デバイス インターフェイスの名前を取得する**します。

[**DRV\_QUERYDEVNODE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536365(v=vs.85))

デバイスの devnode 数を照会します。

[**DRV\_QUERYMAPPABLE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536366(v=vs.85))

デバイスが、マッパーで使用できるかどうかを照会します。

[**DRVM\_MAPPER\_CONSOLEVOICECOM\_GET**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536361(v=vs.85))

詳細については、次を参照してください。[音声通信デバイス ID の優先](preferred-voice-communications-device-id.md)します。

[**DRVM\_マッパー\_優先\_取得**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536362(v=vs.85))

詳細については、次を参照してください。[優先デバイス ID にアクセスする](accessing-the-preferred-device-id.md)します。

 

 




