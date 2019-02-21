---
title: デバイスのインターフェイス名を取得します。
description: デバイスのインターフェイス名を取得します。
ms.assetid: 2ad0bafa-c836-4dca-9287-72cdbddec7d0
keywords:
- WDM オーディオ拡張 WDK、デバイス インターフェイス名
- デバイス インターフェイス名の WDK オーディオ
- インターフェイス名の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbdb0c8235e53c71aefe84e397d0288055dce0de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549656"
---
# <a name="obtaining-a-device-interface-name"></a>デバイスのインターフェイス名を取得します。


## <span id="obtaining_a_device_interface_name"></span><span id="OBTAINING_A_DEVICE_INTERFACE_NAME"></span>


Windows 2000 以降、Windows のマルチ メディア機能と Windows Me で**waveInMessage**、 **waveOutMessage**、 **midiInMessage**、 **midiOutMessage**、および**mixerMessage**デバイスのデバイスのインターフェイスの名前を取得できます。 この情報は、waveIn、waveOut、midiIn midiOut、またはミキサー API 以外のデバイスを識別するために必要なアプリケーション プログラムに役立ちます。 これらの Api のいずれか、デバイス ID で十分です。

プラグ アンド プレイのマネージャーには、それを列挙する各デバイスを一意に識別するデバイス インターフェイス名が生成されます。 アプリケーションでは、不透明なとしてデバイス インターフェイス名を含む文字列を扱う必要があります。 デバイス インターフェイスの詳細については、次を参照してください。[デバイス インターフェイスの概要](https://msdn.microsoft.com/library/windows/hardware/ff549460)します。

Mmddk.h ヘッダー ファイルには、デバイス インターフェイス名を取得するための 2 つのメッセージ定数を定義します。

[**DRV\_QUERYDEVICEINTERFACESIZE**](https://msdn.microsoft.com/library/windows/hardware/ff536364)

[**DRV\_QUERYDEVICEINTERFACE**](https://msdn.microsoft.com/library/windows/hardware/ff536363)

最初のメッセージは、デバイス インターフェイス名を含む文字列を保持するために必要なバッファーのバイト単位のサイズを取得します。 2 番目のメッセージは、必要なサイズのバッファーに名の文字列を取得します。

システムをインターセプトし、処理、DRV\_QUERYDEVICEINTERFACESIZE と DRV\_デバイス ドライバーへのメッセージを送信することがなく QUERYDEVICEINTERFACE メッセージ。

最初のパラメーター、 *xxx*メッセージ関数は、デバイス ID を呼び出し元は、適切なハンドルの型にキャストする必要があります。HWAVEIN、HWAVEOUT、HMIDIIN、HMIDIOUT、または HMIXER します。 詳細については、 *xxx*メッセージ関数を参照してください[System-Intercepted デバイス メッセージ](system-intercepted-device-messages.md)します。

 

 




