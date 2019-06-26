---
title: デバイス インターフェイス名の取得
description: デバイス インターフェイス名の取得
ms.assetid: 2ad0bafa-c836-4dca-9287-72cdbddec7d0
keywords:
- WDM オーディオ拡張 WDK、デバイス インターフェイス名
- デバイス インターフェイス名の WDK オーディオ
- インターフェイス名の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1c32b7f1cba184099f2a7decf64447a0a0116b9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355338"
---
# <a name="obtaining-a-device-interface-name"></a>デバイス インターフェイス名の取得


## <span id="obtaining_a_device_interface_name"></span><span id="OBTAINING_A_DEVICE_INTERFACE_NAME"></span>


Windows 2000 以降、Windows のマルチ メディア機能と Windows Me で**waveInMessage**、 **waveOutMessage**、 **midiInMessage**、 **midiOutMessage**、および**mixerMessage**デバイスのデバイスのインターフェイスの名前を取得できます。 この情報は、waveIn、waveOut、midiIn midiOut、またはミキサー API 以外のデバイスを識別するために必要なアプリケーション プログラムに役立ちます。 これらの Api のいずれか、デバイス ID で十分です。

プラグ アンド プレイのマネージャーには、それを列挙する各デバイスを一意に識別するデバイス インターフェイス名が生成されます。 アプリケーションでは、不透明なとしてデバイス インターフェイス名を含む文字列を扱う必要があります。 デバイス インターフェイスの詳細については、次を参照してください。[デバイス インターフェイスの概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-interface-classes)します。

Mmddk.h ヘッダー ファイルには、デバイス インターフェイス名を取得するための 2 つのメッセージ定数を定義します。

[**DRV\_QUERYDEVICEINTERFACESIZE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536364(v=vs.85))

[**DRV\_QUERYDEVICEINTERFACE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536363(v=vs.85))

最初のメッセージは、デバイス インターフェイス名を含む文字列を保持するために必要なバッファーのバイト単位のサイズを取得します。 2 番目のメッセージは、必要なサイズのバッファーに名の文字列を取得します。

システムをインターセプトし、処理、DRV\_QUERYDEVICEINTERFACESIZE と DRV\_デバイス ドライバーへのメッセージを送信することがなく QUERYDEVICEINTERFACE メッセージ。

最初のパラメーター、 *xxx*メッセージ関数は、デバイス ID を呼び出し元は、適切なハンドルの型にキャストする必要があります。HWAVEIN、HWAVEOUT、HMIDIIN、HMIDIOUT、または HMIXER します。 詳細については、 *xxx*メッセージ関数を参照してください[System-Intercepted デバイス メッセージ](system-intercepted-device-messages.md)します。

 

 




