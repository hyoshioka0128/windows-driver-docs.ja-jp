---
title: MIDI のオーディオ デバイス メッセージ
description: MIDI のオーディオ デバイス メッセージ
ms.assetid: d3b00985-6894-41ea-b493-d0aee269d5bf
ms.date: 04/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: c86b7310e067ddc867ae01fa710a9f5ef60f9563
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925505"
---
# <a name="audio-device-messages-for-midi"></a>MIDI のオーディオ デバイス メッセージ


Windows XP 以降のバージョンの Windows (Windows Vista を含む) では、オペレーティングシステムはオーディオデバイスメッセージを使用して、音楽楽器 digital interface (MIDI) 入出力ドライバーと通信します。

すべての MIDI 入力および出力ドライバーには、ドライバーを有効または無効にするための[Driverproc](https://docs.microsoft.com/windows/win32/api/mmiscapi/nc-mmiscapi-driverproc)エントリポイント関数が1つ必要です。 さらに、Windows オペレーティングシステムからのメッセージを処理するためのエントリポイント関数が追加されている必要があります。 MIDI 出力ドライバーの場合、追加のエントリポイント関数は[**Modmessage**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537532(v=vs.85))です。これは、midi デバイスの製造元によって提供される必要があります。 この関数は、WINMM.DLL が MIDI 出力ドライバーに送信するメッセージを処理します。 WINMM.DLL は、オペレーティングシステムと MIDI 出力ドライバーが相互に通信するのに役立つ関数を含む Windows ダイナミックリンクライブラリ (DLL) モジュールです。 具体的には、WINMM.DLL は、Windows 上で実行される16ビットマルチメディアアプリケーションを管理するのに役立ちます。

**Modmessage**関数によって受信される各メッセージには、dword 変数 (\_dword PTR) への2つのポインターが含まれています。 一部のメッセージでは、これらのパラメーターのいずれかが、クライアントからの追加情報を含む構造体を指しているか、またはドライバーがクライアントの情報を格納するための空の構造体を指しています。 このような構造の一例として、 [**Midiopendesc**](https://docs.microsoft.com/windows/desktop/api/mmddk/ns-mmddk-midiopendesc_tag)があります。 MIDI 出力デバイスドライバーで使用されるその他の2つの構造体は、Windows SDK で説明されています。 これらの構造の詳細については、「 [Midihdr](https://docs.microsoft.com/windows/win32/api/mmeapi/ns-mmeapi-midihdr)と[Midioutcap](https://docs.microsoft.com/windows/win32/api/mmeapi/ns-mmeapi-midioutcaps)」を参照してください。

次に、オーディオデバイスのメッセージと、それらを MIDI 出力ドライバー用に処理する**Modmessage** entry point 関数の一覧を示します。

[**modMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537532(v=vs.85))

[**MODM\_CACHEDRUMPATCHES**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537533(v=vs.85))

[**MODM\_キャッシュパッチ**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537534(v=vs.85))

[**MODM\_データ**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537535(v=vs.85))

[**MODM\_GETDEVCAPS**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537536(v=vs.85))

[**MODM\_GETNUMDEVS**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537537(v=vs.85))

[**MODM\_GETPOS**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537538(v=vs.85))

[**MODM\_GETVOLUME**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537539(v=vs.85))

[**MODM\_LONGDATA**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537540(v=vs.85))

[**MODM\_オープン**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537541(v=vs.85))

[**MODM\_一時停止**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537542(v=vs.85))

[**MODM\_準備**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537543(v=vs.85))

[**MODM\_プロパティ**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537544(v=vs.85))

[**MODM\_リセット**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537545(v=vs.85))

[**MODM\_の再起動**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537546(v=vs.85))

[**MODM\_SETVOLUME**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537547(v=vs.85))

[**MODM\_停止**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537548(v=vs.85))

[**MODM\_STRMDATA**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537549(v=vs.85))

[**MODM\_UNPREPARE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537550(v=vs.85))

[**MOM\_の終了**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537551(v=vs.85))

[**MOM\_完了**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537552(v=vs.85))

[**MOM\_を開く**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537553(v=vs.85))

 

 





