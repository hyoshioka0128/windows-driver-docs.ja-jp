---
title: 処理の停止のデバッグ
description: 処理の停止のデバッグ
ms.assetid: 9dff37ed-4843-4e85-8ab3-6a0a37a58c23
keywords:
- ストリーミングの停止を処理、デバッグ、ビデオ ストリーム失速カーネル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0051d7ae2a9f4aa5eddc1a7efe3b47bfdcef71d0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324561"
---
# <a name="debugging-a-processing-stall"></a>処理の停止のデバッグ


関連する暗証番号 (pin) を検索することから始めます。 関連するビデオのキャプチャの暗証番号 (pin) がアドレスを仮想的な場合は、 **8160DDE0**ので、使用して、 [ **! ks.dump** ](-ks-dump.md)このアドレスでの拡張機能コマンドの詳細を取得します。

```dbgcmd
kd> !ks.dump 8160DDE0 7
Pin object 8160DDE0 [CKsPin = 8160DD50]
    DeviceState    KSSTATE_RUN
    ClientState    KSSTATE_RUN
    CKsPin object 8160DD50 [KSPIN = 8160DDE0]
        State                    KSSTATE_RUN
        Processing Mutex         8160DFD0 is not held
        And Gate &               8160DF88
        And Gate Count           1
```

まず、ピンが適切な状態、および処理ミュー テックスを別のスレッドによって保持されているかどうかを決定します。 暗証番号 (pin) の状態は、この場合、 **KSSTATE\_実行**必要があるし、処理のミュー テックスが保持されていない、次に使用して、 [ **! ks.dumpqueue** ](-ks-dumpqueue.md)拡張機能使用可能なフレームがあるかどうかを判断するには。

```dbgcmd
kd> !ks.dumpqueue 8160DDE0 7
Queue 8172D5D8:
 Frames Received  : 763
    Frames Waiting   : 5
...<this part of display not shown>...
Queue 8172D5D8:
 Frame Header 81B77E60:
        Irp = 816EE008
        Refcount = 1
    Frame Header 81A568D0:
        Irp = 816DE008
        Refcount = 0
    Frame Header 81844ED8:
        Irp = FFA0F650
        Refcount = 0
    Frame Header 8174B0B0:
        Irp = FFABB460
        Refcount = 0
    Leading Edge:
        Stream Pointer 8183EA58 [Public 8183EA90]:
            Frame Header = 81B77E60
...<this part of display not shown>...
```

部分的な上の画面で、 **! ks.dumpqueue** 5 つのフレームがあることがわかります出力を待機中、または使用可能な。 これらのフレームの先行またはリーディング エッジの背後にあるか? **! Ks.dumpqueue**を表示するフレームが古いものから順に常に一覧表示します。 この一覧を表示すると、最初のフレーム、最も古いフレームのリーディング エッジのフレームのヘッダーと一致します。 したがって、最先端のすべての利用可能なフレーム、います。

、そうでないこのポインターを複製する期限のカウントの参照を保持するいたし、最先端の背後にあるされたすべてのフレームの代わりに、問題はほとんどの場合、ハードウェアまたはハードウェアのドライバーのプログラミングのいずれかで生成されます。 ハードウェアが (チェックの割り込みおよび Dpc) のバッファー入力候補をシグナル通知するかどうかを確認し、ドライバーが応答している適切にこれらの通知を (たとえば、バッファーの完了時に複製を削除する) ことによって判断します。

この例のようにすべてのフレームがリーディング エッジの前、問題、ほぼ間違いなくソフトウェア問題です。 詳細情報は、暗証番号 (pin) を調べることで取得することができ、ゲートします。

### <a name="span-idinterpretingtheandgatespanspan-idinterpretingtheandgatespaninterpreting-the-and-gate"></a><span id="interpreting_the_and_gate"></span><span id="INTERPRETING_THE_AND_GATE"></span>解釈、およびゲート

Pin のおよびゲート コントロールを処理します。 ゲートの数が 1 つの場合は、処理が発生することができます。 使用して、and ゲートの現在の状態を取得、 **! ks.dump**拡張機能。

```dbgcmd
kd> !ks.dump 8160DDE0 7
Pin object 8160DDE0 [CKsPin = 8160DD50]
    DeviceState    KSSTATE_RUN
    ClientState    KSSTATE_RUN
    CKsPin object 8160DD50 [KSPIN = 8160DDE0]
        State                    KSSTATE_RUN
        Processing Mutex         8160DFD0 is not held
        And Gate &               8160DF88
        And Gate Count           1
```

ゲート数は、1 つであるため、ゲートは開いています。 この場合、処理の停止の次の潜在的な原因を調べます。

-   プロセスのディスパッチで状態が正しく返される\_保留します。

-   データ可用性大文字と小文字が不足している、 [KsPinAttemptProcessing](https://go.microsoft.com/fwlink/p/?linkid=56545)呼び出します。

 

 





