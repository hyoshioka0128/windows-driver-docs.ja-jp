---
title: ご利用のシンセサイザーをレガシ デバイスとして公開
description: ご利用のシンセサイザーをレガシ デバイスとして公開
ms.assetid: 25e5e14f-1db5-45dc-9048-674420d79824
keywords:
- シンセサイザー WDK オーディオ、レガシ デバイス
- デバイスのレガシ サポート WDK DirectMusic
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40b7a6c4b531f921215d419f8053f43e6f8c4e22
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333653"
---
# <a name="exposing-your-synthesizer-as-a-legacy-device"></a>ご利用のシンセサイザーをレガシ デバイスとして公開


## <span id="exposing_your_synthesizer_as_a_legacy_device"></span><span id="EXPOSING_YOUR_SYNTHESIZER_AS_A_LEGACY_DEVICE"></span>


DirectMusic デバイスとレガシ MIDI デバイスの両方として、シンセサイザー ハードウェアを公開する 1 つのデバイス ドライバーを作成したい場合があります (つまり、Windows のマルチ メディア midiOut を通じて*Xxx* API)。 この手法は、次の 3 つのケースで役立ちます。

1.  デバイスが配布リストをサポートしていない場合。 例としては、片方のドライバー (Windows ドライバー キットの mpu401 サンプルを参照して\[WDK\]) を設定すると、ROM のみを持つデバイスとソフトウェアの固定機能シンセサイザー (たとえば、FM)。

    この場合、デバイスでは、レガシ MIDI インターフェイスに加え、DirectMusic インターフェイスを公開できます。 1 つだけのレガシ MIDI pin を公開します。 WDM オーディオをレガシ MIDI デバイスとして列挙できるように、従来のインターフェイスの pin、リストの先頭に重要です。

2.  デバイスがサポートして場合 DLS、電源を読み込まれた状態にします。 このデバイスは、DL と GM/GS/XG wave テーブルを含む ROM の両方の RAM を持っています。

    この場合、デバイスは両方のインターフェイスも公開できます。 2 つのインターフェイスは相互に排他的である場合 (つまり、1 回ものをダウンロードする場合、ROM が表示されない) し、ピンが 1 つ (2 つの pin) ではなく選択できる 2 つのインターフェイスを持つ必要があります。

3.  デバイスがの DL が入る「空」(たとえば、DirectMusic ソフトウェア シンセサイザー) はサポートし、DLS 必要があるその wave テーブルを初期化するためにダウンロードします。

    この初期化は、デバイスが配布リスト (たとえば、ROM に設定既定のサンプルがある) 場合のダウンロードを要求していない場合や、DirectMusic 暗証番号 (pin) が開かれている場合は必要ありません (DirectMusic Api は、DL のダウンロードが発生したことを確認します)。

    従来の Api を介して DLS デバイスを公開するには、余分な作業が必要です。 DLS instruments を必要とするデバイスのレガシ暗証番号 (pin) が開かれると、ドライバーを見つけて使用する DLS コレクションを含むファイルを開きます。 ドライバーは、する必要があります、更新プログラムと銀行口座の変更をインターセプトし、DLS ファイルから適切なデータを取得、そのデバイスに必要な DLS ダウンロードを実行を。

    この例は、問題のあるため、 [WDMAud システム ドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver)し、その他のクライアントは、コレクションをダウンロードする必要があることに注意してください。 MIDI 更新プログラムの変更とメモの送信の起動だけです。

 

 




