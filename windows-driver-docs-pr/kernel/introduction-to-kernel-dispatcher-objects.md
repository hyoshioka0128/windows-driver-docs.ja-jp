---
title: カーネル ディスパッチャー オブジェクトの概要
description: カーネル ディスパッチャー オブジェクトの概要
ms.assetid: acf7b19a-55a3-4d9b-87ff-ca4df9ed3a45
keywords:
- WDK、カーネル ディスパッチャー オブジェクトは、カーネルのディスパッチャー オブジェクトの概要
- カーネルのディスパッチャー オブジェクトについてのディスパッチャー オブジェクト WDK カーネル
- WDK カーネルの状態を待機します。
- シグナル状態の WDK カーネル
- 非シグナル状態の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d47107a24e2f59dead155879f78fd93bcf47fcb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369726"
---
# <a name="introduction-to-kernel-dispatcher-objects"></a>カーネル ディスパッチャー オブジェクトの概要





カーネルと呼ばれるオブジェクトの型のセットを定義する*カーネルのディスパッチャー オブジェクト*、または単*のディスパッチャー オブジェクト*します。 ディスパッチャー オブジェクトには、タイマー オブジェクトには、イベント オブジェクトには、セマフォ オブジェクトには、ミュー テックス オブジェクトでは、スレッド オブジェクトが含まれます。

ドライバーは IRQL パッシブで実行中に、nonarbitrary スレッド コンテキスト内で同期メカニズムとしてのディスパッチャー オブジェクトを使用することができます\_レベル。

### <a name="dispatcher-object-states"></a>ディスパッチャー オブジェクトの状態

すべてのカーネル定義のディスパッチャー オブジェクト型では、シグナルされたに設定、または Not シグナルされたに設定される状態が。

スレッドのグループがその操作を同期できるは、1 つまたは複数のスレッド呼び出し場合[ **kewaitforsingleobject の 1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)、 [ **KeWaitForMutexObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553344)、または[ **KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects)します。 これらの関数は、別のルーチンまたはスレッドは、1 つまたは複数のディスパッチャー オブジェクトをシグナルされた状態に設定されるまでに、ディスパッチャーとして入力し、待機オブジェクト ポインターを受け取ります。

スレッドを呼び出すと、 **kewaitforsingleobject の 1**ディスパッチャー オブジェクトを待機する (または**KeWaitForMutexObject**ミュー テックスを)、スレッドを入れる、*待機*状態まで、ディスパッチャー オブジェクトは、シグナルされた状態に設定されます。 スレッドを呼び出すことができます**KeWaitForMultipleObjects** 、いずれかのいずれかまたはすべてを待機する、一連のディスパッチャー オブジェクトに設定シグナルされました。

カーネルがそのオブジェクトを待機している任意のスレッドの状態を変更する dispatcher オブジェクトがシグナルされた状態に設定されている場合*準備*します。 (同期のタイマーとの同期イベントは、この規則の例外は、同期イベントまたはタイマーが通知を待機中の 1 つだけのスレッドが準備完了状態に設定されます。 詳細については、次を参照してください[タイマー オブジェクトと Dpc](timer-objects-and-dpcs.md)と[イベント オブジェクト](event-objects.md)。)。準備完了状態のスレッドは、その現在の実行時に従って実行するスケジュールされます[スレッドの優先順位](thread-priorities.md)と優先順位が任意のスレッドのプロセッサの現在の可用性。

### <a name="when-can-drivers-wait-for-dispatcher-objects"></a>ドライバーがのディスパッチャー オブジェクトを待機できる場合をでしょうか。

一般に、ドライバーは、次の状況の少なくとも 1 つが true の場合にのみ設定するディスパッチャー オブジェクトを待機できます。

-   ドライバーは、nonarbitrary スレッド コンテキストで実行しています。

    つまり、待機状態を入力したスレッドを識別できます。 Nonarbitrary スレッド コンテキストで実行する唯一のドライバーのルーチンは、実際には、 [ **DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)、 [ *AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)、 [*を再初期化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-driver_reinitialize)、および[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)ルーチンの任意のドライバーとドライバーの最上位レベルのディスパッチ ルーチン。 これらすべてのルーチンは、システムによって直接呼び出されます。

-   ドライバーでは、完全に同期 I/O 要求を実行します。

    つまり、下にあるドライバーが要求を処理を完了するまでを返します、I/O 要求といないドライバーの処理中にはドライバー キューのすべての操作なし。

さらに、ドライバーがで実行されている場合は、待機状態を入力することはできませんまたは IRQL 上 = ディスパッチ\_レベル。

これらの制限事項に基づき、次の規則を使用する必要があります。

-   **DriverEntry**、 *AddDevice*、*を再初期化*、および*アンロード*任意のドライバーのルーチンのディスパッチャー オブジェクトを待機できます。

-   最上位レベルのドライバーのディスパッチ ルーチンは、ディスパッチャー オブジェクトで待機できます。

-   ドライバーの下位レベルのルーチン、I/O 操作が同期の場合、ディスパッチ オブジェクトの待機、作成など、フラッシュ、シャット ダウン、したり終了したりできます操作や、一部のデバイスの I/O 制御操作をいくつかのディスパッチ PnP ドライバー パッケージと電源を操作します。

-   下位レベルのドライバーのディスパッチ ルーチンは、ディスパッチャー オブジェクトの非同期 I/O 操作が完了するを待つことはできません。

-   IRQL ディスパッチ以上を実行しているドライバー ルーチン\_シグナルされた状態に設定する dispatcher オブジェクトのレベルを待たずする必要があります。

-   ドライバーは、またはページングのデバイスには、転送操作の完了のシグナルされた状態に設定するディスパッチャー オブジェクトを待機する必要がありますしません。

-   ドライバーのディスパッチ ルーチン サービス読み取り/書き込み: 一般的に要求がシグナルされた状態に設定するディスパッチャー オブジェクトを待機できません。

-   デバイス I/O 制御要求のディスパッチ ルーチンに設定するシグナルされた状態場合にのみ、転送の種類の I/O 制御コードはメソッドのディスパッチャー オブジェクトを待機できる\_バッファーに格納されました。

-   SCSI ミニポート ドライバーでは、カーネルのディスパッチャー オブジェクトは使用しないでください。 SCSI ミニポート ドライバーはのみ呼び出す必要があります[SCSI ポート ライブラリ ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

任意のスレッド コンテキストでその他のすべての標準のドライバー ルーチンを実行します。 どのスレッドがキューに置かれた操作を処理する、またはデバイスの割り込みを処理するために、ドライバーのルーチンが呼び出されたときには、現在の。 発生した IRQL のいずれかでディスパッチで最も標準的なドライバーのルーチンを実行するさらに、\_レベル、または DIRQL でのデバイス ドライバー。

必要に応じてのかどうか、ドライバーことができます、ドライバーの他のルーチンが待機できるデバイス専用のスレッドを作成 (ISR を除くまたは[ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)ルーチン) シグナルされた状態にディスパッチャー オブジェクトを設定するには非シグナル状態にリセットします。

一般的なガイドラインとして、新しいデバイス ドライバが I/O 操作中にデバイス状態の変更を待っている間、50 マイクロ秒よりも長い遅延する必要がありますする場合は、デバイス専用のスレッドにドライバーを実装する検討してください。 デバイス ドライバーが最上位レベルのドライバーもある場合は、使用を検討して[システム ワーカー スレッド](system-worker-threads.md)と 1 つまたは複数のワーカー スレッド コールバック ルーチンを実装します。 参照してください[ **PsCreateSystemThread** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pscreatesystemthread)と[ドライバーが作成したスレッドにインタロックされたキューを管理する](managing-interlocked-queues-with-a-driver-created-thread.md)します。

 

 




