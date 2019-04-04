---
title: MIDI のオーディオ デバイス メッセージ
description: MIDI のオーディオ デバイス メッセージ
ms.assetid: d3b00985-6894-41ea-b493-d0aee269d5bf
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4f537882be7a29213af1b2320e6fb48aac4ec6f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575018"
---
# <a name="audio-device-messages-for-midi"></a>MIDI のオーディオ デバイス メッセージ


Windows XP および Windows (Windows Vista を含む) の以降のバージョンでは、オペレーティング システムと通信楽器デジタル インターフェイス (MIDI) 入力と出力のドライバーのオーディオ デバイス メッセージを使用しています。

MIDI すべての入力し、出力のドライバーが 1 つの[DriverProc](https://go.microsoft.com/fwlink/p/?linkid=142258)エントリ ポイントを有効にまたはドライバーを無効にします。 さらに、Windows オペレーティング システムから、追加のエントリ ポイント関数メッセージを処理するために必要です。 MIDI 出力のドライバーの場合、追加のエントリ ポイント関数は[ **modMessage**](https://msdn.microsoft.com/library/windows/hardware/ff537532)、これは、MIDI デバイスの製造元によって提供される必要があります。 この関数は、MIDI 出力ドライバーに WINMM を送信するメッセージを処理します。 WINMM は、オペレーティング システムと相互通信、MIDI 出力ドライバーに役立つ関数が含まれた Windows ダイナミック リンク ライブラリ (DLL) モジュールです。 具体的には、WINMM は、Windows 上で実行される 16 ビットのマルチ メディア アプリケーションの管理に役立ちます。

受信した各メッセージ、 **modMessage**関数は、DWORD 変数に 2 つのポインターられて (DWORD\_PTR)。 一部のメッセージについて、クライアントから追加情報を格納する構造体を指すこれらのパラメーターのいずれかまたはドライバーに、クライアントの情報を格納するための空の構造体を指します。 このような構造体の 1 つの例は、 [ **MIDIOPENDESC**](https://msdn.microsoft.com/library/windows/hardware/ff537518)します。 MIDI 出力デバイス ドライバーによって使用されるその他の 2 つの構造があるし、Windows SDK で説明しています。 これらの構造体の詳細については、[MIDIHDR](https://go.microsoft.com/fwlink/p/?linkid=142406)と[MIDIOUTCAPS](https://go.microsoft.com/fwlink/p/?linkid=142347)を参照してください。

オーディオ デバイス メッセージの一覧を次に、 **modMessage** MIDI ドライバーの出力の処理関数のエントリ ポイント。

[**modMessage**](https://msdn.microsoft.com/library/windows/hardware/ff537532)

[**器\_CACHEDRUMPATCHES**](https://msdn.microsoft.com/library/windows/hardware/ff537533)

[**器\_CACHEPATCHES**](https://msdn.microsoft.com/library/windows/hardware/ff537534)

[**器\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff537535)

[**器\_GETDEVCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff537536)

[**MODM\_GETNUMDEVS**](https://msdn.microsoft.com/library/windows/hardware/ff537537)

[**器\_GETPOS**](https://msdn.microsoft.com/library/windows/hardware/ff537538)

[**器\_GETVOLUME**](https://msdn.microsoft.com/library/windows/hardware/ff537539)

[**器\_LONGDATA**](https://msdn.microsoft.com/library/windows/hardware/ff537540)

[**器\_開く**](https://msdn.microsoft.com/library/windows/hardware/ff537541)

[**器\_一時停止**](https://msdn.microsoft.com/library/windows/hardware/ff537542)

[**器\_準備**](https://msdn.microsoft.com/library/windows/hardware/ff537543)

[**器\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/ff537544)

[**MODM\_RESET**](https://msdn.microsoft.com/library/windows/hardware/ff537545)

[**器\_再起動**](https://msdn.microsoft.com/library/windows/hardware/ff537546)

[**器\_とる**](https://msdn.microsoft.com/library/windows/hardware/ff537547)

[**器\_停止**](https://msdn.microsoft.com/library/windows/hardware/ff537548)

[**器\_STRMDATA**](https://msdn.microsoft.com/library/windows/hardware/ff537549)

[**器\_UNPREPARE**](https://msdn.microsoft.com/library/windows/hardware/ff537550)

[**MOM\_閉じる**](https://msdn.microsoft.com/library/windows/hardware/ff537551)

[**MOM\_完了**](https://msdn.microsoft.com/library/windows/hardware/ff537552)

[**MOM\_開く**](https://msdn.microsoft.com/library/windows/hardware/ff537553)

 

 





