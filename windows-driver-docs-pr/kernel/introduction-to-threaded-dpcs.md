---
title: スレッドの Dpc の概要
description: スレッドの Dpc の概要
ms.assetid: 891a8a52-83ff-400a-9477-8edca1b9a83c
keywords:
- スレッドの Dpc WDK カーネル
- リアルタイムのスレッドの WDK カーネル
- 割り込まれた Dpc WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b57f17caa1b966ec79273d6456b041b1e2286cea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550162"
---
# <a name="introduction-to-threaded-dpcs"></a>スレッドの Dpc の概要





スレッドの Dpc は、Windows Vista および Windows の以降のバージョンで使用できます。

A*スレッド DPC* IRQL でシステムを実行する DPC はパッシブ =\_レベル。 既定では、スレッド Dpc が有効になっているが、設定によって無効にできます、 **HKLM\\システム\\CCS\\コントロール\\sessionmanager で致命的\\カーネル\\ThreadDpcEnable**レジストリ キーを 0 にします。 スレッド Dpc を無効にすると、通常 Dpc として実行されます。

通常の DPC は、すべてのスレッドの実行に横取りされし、もう 1 つの DPC、スレッドによって割り込まれることはできません。 システムがある場合は、キューに置かれた通常 Dpc の数が多い、または任意の長さの時間のすべてのスレッドを一時停止したままになりますこれら Dpc のいずれかを長時間実行する場合。 したがって、通常各 DPC には、オーディオまたはビデオの再生などの時間を区別するアプリケーションのパフォーマンスが低下することがシステムの待機時間が増加します。

逆に、スレッド DPC は他のスレッドではなくが、通常、DPC、によって割り込まれることができます。 そのため、通常 Dpc ではなく、スレッド Dpc を使用する必要があります: DPC を特定する必要があります割り込むことはできませんであっても別の DPC しない限り、します。

システムとしてスレッド Dpc (および通常 Dpc) を表す[ **KDPC** ](https://msdn.microsoft.com/library/windows/hardware/ff551882)構造体。 初期化するために、 **KDPC**スレッド DPC、呼び出しの構造、 [ **KeInitializeThreadedDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff552166)ルーチンを渡して、 [ *CustomThreadedDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542976) DPC の処理を実行するルーチン。

*CustomThreadedDpc*ルーチンがパッシブのいずれかで実行できる\_レベルまたはディスパッチ\_レベル、することが必要、 *CustomThreadedDpc*ルーチン正しく両方の Irql で同期します。 これを行う方法の詳細については、[同期とスレッド Dpc](synchronization-and-threaded-dpcs.md)を参照してください。

さらに、することが必要、 *CustomThreadedDpc*ルーチンのディスパッチのすべての制限に従う\_レベルのコード。 IRQL で実行スレッド Dpc が有効な場合、パッシブ =\_レベルが通常 Dpc と同じ制限される可能性があります。 すべてのスレッドの DPC で実行されるコード-によって呼び出されるすべての関数を含む、 *CustomThreadedDpc*ルーチン — DPC 環境の制限に準拠する必要があります。 たとえば、コード ブロックしないでパッシブ レベルの同期オブジェクトでなど[KEVENT オブジェクト](defining-and-using-an-event-object.md)します。 ネットワーク、ストレージ、および、USB などに、ほとんどの既存デバイス スタックは、スレッドの DPC の処理をサポートしていませんし、パッシブで呼び出されることを検出した場合にブロックを試みる可能性があります\_レベル。 同様の理由で、[カーネル モード ドライバー フレームワーク](https://msdn.microsoft.com/library/windows/hardware/ff544296)(KMDF) は、スレッドの DPC の処理をサポートしていませんし、KMDF ドライバーはスレッド Dpc を使用しようとはしないでください。 DPC 環境の詳細については、[書き込み DPC ルーチン](writing-dpc-routines.md)を参照してください。

スレッド DPC を DPC キューに追加するには、呼び出す[ **KeInsertQueueDpc**](https://msdn.microsoft.com/library/windows/hardware/ff552185)します。 実行前に、スレッド DPC をキューから削除するには、呼び出す[ **KeRemoveQueueDpc**](https://msdn.microsoft.com/library/windows/hardware/ff553169)します。

 

 




