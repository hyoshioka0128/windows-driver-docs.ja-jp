---
title: MIDI のオーディオ デバイス メッセージ
description: MIDI のオーディオ デバイス メッセージ
ms.assetid: d3b00985-6894-41ea-b493-d0aee269d5bf
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f082a76f1ffad1eb4993aed573b58d99769fd62a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355737"
---
# <a name="audio-device-messages-for-midi"></a>MIDI のオーディオ デバイス メッセージ


Windows XP および Windows (Windows Vista を含む) の以降のバージョンでは、オペレーティング システムと通信楽器デジタル インターフェイス (MIDI) 入力と出力のドライバーのオーディオ デバイス メッセージを使用しています。

MIDI すべての入力し、出力のドライバーが 1 つの[DriverProc](https://go.microsoft.com/fwlink/p/?linkid=142258)エントリ ポイントを有効にまたはドライバーを無効にします。 さらに、Windows オペレーティング システムから、追加のエントリ ポイント関数メッセージを処理するために必要です。 MIDI 出力のドライバーの場合、追加のエントリ ポイント関数は[ **modMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537532(v=vs.85))、これは、MIDI デバイスの製造元によって提供される必要があります。 この関数は、MIDI 出力ドライバーに WINMM を送信するメッセージを処理します。 WINMM は、オペレーティング システムと相互通信、MIDI 出力ドライバーに役立つ関数が含まれた Windows ダイナミック リンク ライブラリ (DLL) モジュールです。 具体的には、WINMM は、Windows 上で実行される 16 ビットのマルチ メディア アプリケーションの管理に役立ちます。

受信した各メッセージ、 **modMessage**関数は、DWORD 変数に 2 つのポインターられて (DWORD\_PTR)。 一部のメッセージについて、クライアントから追加情報を格納する構造体を指すこれらのパラメーターのいずれかまたはドライバーに、クライアントの情報を格納するための空の構造体を指します。 このような構造体の 1 つの例は、 [ **MIDIOPENDESC**](https://docs.microsoft.com/windows/desktop/api/mmddk/ns-mmddk-midiopendesc_tag)します。 MIDI 出力デバイス ドライバーによって使用されるその他の 2 つの構造があるし、Windows SDK で説明しています。 これらの構造体の詳細については、次を参照してください。 [MIDIHDR](https://go.microsoft.com/fwlink/p/?linkid=142406)と[MIDIOUTCAPS](https://go.microsoft.com/fwlink/p/?linkid=142347)します。

オーディオ デバイス メッセージの一覧を次に、 **modMessage** MIDI ドライバーの出力の処理関数のエントリ ポイント。

[**modMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537532(v=vs.85))

[**器\_CACHEDRUMPATCHES**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537533(v=vs.85))

[**器\_CACHEPATCHES**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537534(v=vs.85))

[**器\_データ**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537535(v=vs.85))

[**器\_GETDEVCAPS**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537536(v=vs.85))

[**MODM\_GETNUMDEVS**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537537(v=vs.85))

[**器\_GETPOS**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537538(v=vs.85))

[**器\_GETVOLUME**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537539(v=vs.85))

[**器\_LONGDATA**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537540(v=vs.85))

[**器\_開く**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537541(v=vs.85))

[**器\_一時停止**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537542(v=vs.85))

[**器\_準備**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537543(v=vs.85))

[**器\_プロパティ**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537544(v=vs.85))

[**MODM\_RESET**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537545(v=vs.85))

[**器\_再起動**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537546(v=vs.85))

[**器\_とる**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537547(v=vs.85))

[**器\_停止**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537548(v=vs.85))

[**器\_STRMDATA**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537549(v=vs.85))

[**器\_UNPREPARE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537550(v=vs.85))

[**MOM\_閉じる**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537551(v=vs.85))

[**MOM\_完了**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537552(v=vs.85))

[**MOM\_開く**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537553(v=vs.85))

 

 





