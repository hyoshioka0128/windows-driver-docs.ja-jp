---
title: シンセサイザーと Wave シンク
description: シンセサイザーと Wave シンク
ms.assetid: ddcb847e-d46e-4860-9be9-4480e5a6b710
keywords:
- DirectMusic カスタム レンダリング WDK のオーディオ、シンセサイザー
- ユーザー モードの WDK オーディオ、シンセサイザーでカスタムの表示
- ユーザー モードの WDK オーディオ、wave カスタム レンダリング シンクします。
- wave シンク WDK オーディオ、ユーザー モード
- カスタムのシンセサイザー WDK オーディオ、DirectMusic アーキテクチャ
- WDK のオーディオのカスタム レンダリング DirectMusic、wave シンクします。
- ユーザー モード シンセサイザー WDK オーディオ、DirectMusic アーキテクチャ
- ユーザー モード wave シンク WDK オーディオ
- wave の既定のシンク
- 既定のシンセサイザー
- カスタム wave シンク WDK オーディオ
- シンセサイザー WDK オーディオでは、ユーザー モードのシンセサイザーについて
- WDK のオーディオのレンダリング エンジン
- DirectMusic WDK オーディオ、シンセサイザー
- Dmu ポート ドライバー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7be4a2c764744162576bdcb75d37d268cabe877
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335307"
---
# <a name="synthesizers-and-wave-sinks"></a>シンセサイザーと Wave シンク


## <span id="synthesizers_and_wave_sinks"></span><span id="SYNTHESIZERS_AND_WAVE_SINKS"></span>


レンダリング エンジンでは、2 つの部分があります。

-   シンセサイザー、MIDI をとりますがメッセージを wave オーディオ サンプルに変換します。

-   Wave サンプルとは、変換先を提供する wave シンクは、出力を同期します。

既定では、DirectMusic アプリケーションは、wave 出力デバイスとして、シンセサイザーと DirectSound として (dmsynth.dll) のシンセサイザーの Microsoft ソフトウェアを使用します。

DirectX 6.1 と DirectX 7 で DirectMusic アプリケーションは、これらの既定値をオーバーライドできます。 たとえば、シンセサイザーの Microsoft ソフトウェアを使用して、可能性がありますが、.wav ファイルに出力アプリケーションまたは既定 wave シンクで動作するカスタム シンセサイザーを実装できます。 後者のシナリオは、既定 wave シンクは、ほとんどシンセサイザーに対しても有効であるために可能性が高くなります。

DirectX 8 以降では、DirectMusic は常に、ユーザー モード シンセサイザーからデータを出力する組み込み wave シンクを使用が、アプリケーションは、既定のソフトウェアのシンセサイザーをオーバーライドできます。 つまり、DirectMusic アプリケーションは、カスタムのユーザー モード シンセサイザーを実装できますが、シンセサイザー DirectMusic の組み込み wave シンクを使用する必要があります。

Wave シンクし、次の図が DirectMusic アーキテクチャがユーザー モードのシンセサイザーを組み込む方法を示しています。 次の図に"DirectMusic Port"というラベルの付いたブロックがカーネル モードと混同されていない必要がありますに注意してください。 [Dmu ポート ドライバー](dmus-port-driver.md) PortCls システム ドライバー モジュールでは、portcls.sys します。 DirectMusic ポートが使用して、ユーザー モード オブジェクト、 **IDirectMusicPort** (DirectMusic API の一部) のインターフェイス、dmusic.dll に実装されます。 DirectMusic ポートの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

![シンクのシンセサイザーのユーザー モードおよび wave directmusic アーキテクチャを示す図](images/dmblock.png)

上記の図では、アプリケーションは、データを wave データに、ノートを表示するためにソフトウェア シンセサイザー (既定で dmsynth.dll) までのデータ (MIDI または DLS) を通過するユーザー モード DirectMusic ポートに送信します。 Wave シンクでは、タイミングを管理し、シンセサイザー大量のデータを受信する準備ができた場合にバッファーを渡します。 シンセサイザーのバッファーがいっぱい (、 **IDirectSoundBuffer**既定ではオブジェクト) データのため、it は DirectSound に渡すことができます。 DirectSound は、データを再生するか、 [KMixer システム ドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver) DirectSound ハードウェア アクセラレータによるレンダリング pin を通じて上で再生、オーディオ デバイスを 1 つが使用可能な場合または (を参照してください[DirectSound ハードウェアの概要高速化](overview-of-directsound-hardware-acceleration.md))。

この同じ基本アーキテクチャは、例外、KMixer システム ドライバーやハードウェアに直接 wave シンクがデータ バッファーを渡すことで、カーネル モードの実装にも適用されます。 Dmu ポート ドライバーでは、カーネル モード ソフトウェアのシンセサイザーのウェーブ シンクを実装します。 詳細については、次を参照してください。 [A Wave シンクがカーネル モードのソフトウェアのシンセサイザーの](a-wave-sink-for-kernel-mode-software-synthesizers.md)します。

次の手順が完了したら、ユーザー モード DirectMusic ポートはオープンで使用するためにアクティブ化します。 このドライバー コードの多くは動作するいるとすぐに機能の実装を開始できます。 ユーザー モードの Microsoft ソフトウェアのシンセサイザーのソース コードをテンプレートとして使用し、新しい機能の追加を開始します。

シンセサイザーのユーザー モード ソフトウェアをオブジェクトとして実装できる、 [IDirectMusicSynth](https://msdn.microsoft.com/library/windows/hardware/ff536519)インターフェイス。 ユーザー モードのウェーブ シンクを持つオブジェクトとして実装できる、 [IDirectMusicSynthSink](https://msdn.microsoft.com/library/windows/hardware/ff536520)インターフェイス。 詳細については、次を参照してください。 [IDirectMusicSynth と IDirectMusicSynthSink](idirectmusicsynth-and-idirectmusicsynthsink.md)します。

 

 




