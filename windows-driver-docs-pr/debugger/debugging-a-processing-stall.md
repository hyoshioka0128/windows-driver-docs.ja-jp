---
title: 処理の停止のデバッグ
description: 処理の停止のデバッグ
ms.assetid: 9dff37ed-4843-4e85-8ab3-6a0a37a58c23
keywords:
- カーネルストリーミングデバッグ, ビデオストリームの停止, 処理の停止
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 088a6a8f5dcb069b0d64ed73ce717aab4fa483df
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534781"
---
# <a name="debugging-a-processing-stall"></a>処理の停止のデバッグ


まず、関連する pin を見つけます。 架空のケースでは、関連するビデオキャプチャピンのアドレスは**80**になります。そのため、このアドレスに対して[**! ks. dump**](-ks-dump.md) extension コマンドを使用して詳細情報を取得します。

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

まず、pin が適切な状態であるかどうか、および処理ミューテックスが別のスレッドによって保持されているかどうかを確認します。 この場合、pin の状態は**Ksk state \_ RUN**である必要がありますが、処理ミューテックスは保持されていないため、次に[**! ks キュー**](-ks-dumpqueue.md)拡張機能を使用して、使用可能なフレームがあるかどうかを確認します。

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

上の例では、 **! ks キュー**の出力が部分的に表示されています。5つのフレームが待機中であるか、使用可能であることがわかります。 これらのフレームは、先頭のエッジの前または後ろにありますか。 **! Ks キュー**の表示では、フレームは常に古いものから最新のものに一覧表示されます。 先頭のエッジのフレームヘッダーは、最も古いフレームで示されている最初のフレームと一致します。 このため、使用可能なすべてのフレームが最先端になります。

そうではなく、すべてのフレームが先頭エッジの背後にあり、複製ポインターによる参照カウントを持っている場合は、ハードウェアまたはドライバーによるハードウェアのプログラミングに起因する可能性が最も高い問題が発生します。 ハードウェアが、バッファーの入力候補 (割り込みおよび Dpc をチェック) であることを確認し、ドライバーがこれらの通知に適切に応答していることを確認します (たとえば、バッファーの完了時に複製を削除します)。

この例に示すように、すべてのフレームが最先端のエッジより前にある場合、問題はほぼ確実にソフトウェアの問題です。 Pin のおよびゲートを確認することで、さらに詳しい情報を得ることができます。

### <a name="span-idinterpreting_the_and_gatespanspan-idinterpreting_the_and_gatespaninterpreting-the-and-gate"></a><span id="interpreting_the_and_gate"></span><span id="INTERPRETING_THE_AND_GATE"></span>およびゲートの解釈

Pin のおよびゲートは、処理を制御します。 ゲート数が1の場合は、処理が発生する可能性があります。 **! Ks**拡張子を使用して、およびゲートの現在の状態を取得します。

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

ゲート数が1であるため、ゲートとゲートが開かれています。 この場合は、処理が停止する可能性のある次の原因を調査してください。

-   プロセスディスパッチによって、保留中の状態が誤って返されました \_ 。

-   データの可用性ケースに[KsPinAttemptProcessing](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinattemptprocessing)呼び出しがありません。

 

 





