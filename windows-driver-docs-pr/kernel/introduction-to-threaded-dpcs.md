---
title: スレッド DPC の概要
description: スレッド DPC の概要
ms.assetid: 891a8a52-83ff-400a-9477-8edca1b9a83c
keywords:
- スレッド Dpc WDK のカーネル
- リアルタイムスレッド WDK カーネル
- 割り込まれる Dpc WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66466f956f520d0e381263b42c9900cd1bc01f57
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838618"
---
# <a name="introduction-to-threaded-dpcs"></a>スレッド DPC の概要





スレッド Dpc は、Windows Vista 以降のバージョンの Windows で使用できます。

スレッド化された*dpc*は、システムが IRQL = パッシブ\_レベルで実行する dpc です。 既定では、スレッド Dpc は有効になっていますが、 **HKLM\\システム\\CCS\\コントロール\\SessionManager\\Kernel\\** のレジストリキーを0に設定することによって無効にすることができます。 スレッド Dpc が無効になっている場合は、通常の Dpc として実行されます。

通常の DPC は、すべてのスレッドの実行をプリエンプション、スレッドまたは別の DPC によって割り込まれることはできません。 システムに多数の通常の Dpc がキューに登録されている場合、または Dpc の1つが長時間実行されている場合、すべてのスレッドは長時間にわたって一時停止状態のままになります。 したがって、通常の DPC はそれぞれ、システムの待機時間が増加するため、オーディオやビデオの再生など、時間のかかるアプリケーションのパフォーマンスが低下する可能性があります。

逆に、スレッド化された DPC は通常の DPC によって割り込まれることがありますが、他のスレッドによって割り込まれることはありません。 そのため、特定の dpc が別の DPC であっても割り込まれないようにする場合を除き、通常の Dpc ではなくスレッド Dpc を使用する必要があります。

システムは、スレッド Dpc (および通常の Dpc) を[**Kdpc**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体として表します。 スレッド化された DPC の**Kdpc**構造体を初期化するには、 [**KeInitializeThreadedDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializethreadeddpc)ルーチンを呼び出し、DPC のアクションを実行する[*CustomThreadedDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542976)ルーチンを渡します。

*CustomThreadedDpc*ルーチンは、パッシブ\_レベルまたはディスパッチ\_レベルで実行できるため、両方の IRQLs で*CustomThreadedDpc*ルーチンが正しく同期されていることを確認する必要があります。 その方法の詳細については、「[同期とスレッド dpc](synchronization-and-threaded-dpcs.md)」を参照してください。

また、 *CustomThreadedDpc*ルーチンがディスパッチ\_レベルコードのすべての制限に従うことを確認する必要があります。 スレッド Dpc が有効になっている場合は、IRQL = パッシブ\_レベルで実行されますが、通常の Dpc と同じ制限が適用されます。 スレッド化された DPC ( *CustomThreadedDpc*ルーチンによって呼び出されるすべての関数を含む) で実行されるすべてのコードは、dpc 環境の制限に準拠している必要があります。 たとえば、 [KEVENT オブジェクト](defining-and-using-an-event-object.md)など、パッシブレベルの同期オブジェクトでコードをブロックすることはできません。 ネットワーク、ストレージ、USB などのほとんどの既存のデバイススタックは、スレッド化された DPC 処理をサポートしていません。また、パッシブ\_レベルで呼び出されることを検出した場合は、ブロックしようとする可能性があります。 同様の理由から、[カーネルモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)(kmdf) は、スレッド化された dpc 処理をサポートしていません。 kmdf ドライバーは、スレッド化された dpc を使用しないようにする必要があります。 DPC 環境の詳細については、「 [Dpc ルーチンの記述](writing-dpc-routines.md)」を参照してください。

DPC キューにスレッド DPC を追加するには、 [**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)を呼び出します。 スレッド化された DPC を実行前にキューから削除するには、 [**KeRemoveQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovequeuedpc)を呼び出します。

 

 




