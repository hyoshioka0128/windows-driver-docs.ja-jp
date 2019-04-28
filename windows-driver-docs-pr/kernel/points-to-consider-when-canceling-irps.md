---
title: IRP をキャンセルするときに考慮すべき点
description: IRP をキャンセルするときに考慮すべき点
ms.assetid: 16a47033-7147-43a2-a9f8-a215f7e90ff1
keywords:
- Irp、ガイドラインのキャンセル
- キャンセル ルーチン、ガイドライン
- Irp WDK のキャンセル可能なカーネル
- 現在の状態で WDK Irp
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 61a78aae240bd690a6507e3a3ad9ec555d99f2f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369224"
---
# <a name="points-to-consider-when-canceling-irps"></a>IRP をキャンセルするときに考慮すべき点





このセクションを実装するためのガイドラインをについて説明します、*キャンセル*ルーチンとキャンセル可能な Irp の処理します。 キャンセル可能な Irp の処理の詳細については、次を参照してください。、[キャンセル セーフ IRP のキューのフローの制御](https://go.microsoft.com/fwlink/p/?linkid=57844)します。

### <a name="general-guidelines-for-all-cancel-routines"></a>すべてのキャンセル ルーチンの一般的なガイドライン

ドライバーを呼び出して、いつでもキャンセル スピン ロックを保持する I/O マネージャー*キャンセル*ルーチン。 その結果、すべて*キャンセル*ルーチンにする必要があります。

-   呼び出す[ **IoReleaseCancelSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549550)前に、コントロールを返します。

-   呼び出さない[ **IoAcquireCancelSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548196)を呼び出す場合を除き、 **IoReleaseCancelSpinLock**最初。

-   相互に呼び出す**IoReleaseCancelSpinLock**に各呼び出しに対して**IoAcquireCancelSpinLock**します。

毎回、*キャンセル*ルーチンの呼び出し**IoReleaseCancelSpinLock**、最新の呼び出しによって返される IRQL を渡す必要があります**IoAcquireCancelSpinLock**します。 I/O マネージャーによって取得されたスピン ロックを解放するときに (ときに保持されていると、*キャンセル*ルーチンが呼び出された)、*キャンセル*ルーチンに渡す必要があります**Irp-&gt;CancelIrql**.

ドライバーでは外部ルーチンを呼び出す必要がありますされません (など**IoCompleteRequest**)、デッドロックにつながるために、スピン ロックを保持しているときにします。

### <a href="" id="using-the-queue-defined-by-the-i-o-manager-"></a>I/O マネージャーによって定義されているキューを使用します。

ドライバーは Irp の独自の内部キューを管理しない限り、その*キャンセル*ルーチンは、次のいずれかの可能性がある着信 IRP で呼び出されます。

-   **CurrentIrp**入力対象のデバイス オブジェクトに

-   ターゲット デバイス オブジェクトに関連付けられているデバイスのキュー内のエントリ

ドライバーは Irp の独自の内部キューを管理しない限り、その*キャンセル*ルーチンを呼び出す必要があります[ **KeRemoveEntryDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff553163) IRP 内のエントリがあるかどうかをテストするは入力ターゲット デバイス オブジェクトに関連付けられているデバイスのキュー。 ドライバーの*キャンセル*ルーチン*できません*呼び出す**KeRemoveDeviceQueue**または**KeRemoveByKeyDeviceQueue**が仮定することはできませんできないためです特定の IRP では、デバイスのキュー内の任意の特定位置にあります。

### <a name="current-state-of-the-input-irp"></a>入力 IRP の現在の状態

場合、*キャンセル*ルーチンを呼び出す、ドライバーが既に開始された I/O IRP の処理と、要求が完了する、すぐに、*キャンセル*ルーチンは、システムのキャンセル スピン ロックを解放する必要がありますとコントロールを返します。

入力 IRP の現在の状態が、保留中の場合、*キャンセル*ルーチンは、次を実行する必要があります。

1.  状態が入力の IRP の I/O の状態のブロックを設定\_の中止された**状態**の場合は 0 と**情報**します。

2.  これが保持している、システムのキャンセル スピン ロックを含むスピン ロックを解除します。

3.  呼び出す[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)特定の IRP でします。

### <a name="holding-irps-in-a-cancelable-state"></a>Irp を取り消しできる状態で保持します。

キャンセル可能な状態では IRP を保持するドライバーのルーチンを呼び出す必要があります[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)呼び出す必要がありますと[ **IoSetCancelRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549674)に場合は、そのエントリ ポイントの設定、*キャンセル*IRP の日常的な。 のみそのドライバーのルーチンを呼び出すことの追加サポート ルーチンなど**IoStartPacket**、 **IoAllocateController**、または**ExInterlockedInsert.リスト**ルーチン。

キャンセル可能な Irp を後で処理するドライバーのルーチンでは、IRP は、要求を満たすための操作を開始する前に既にキャンセルされているかどうかを確認する必要があります。 ルーチンを呼び出す必要があります**IoSetCancelRoutine**の場合は、そのエントリ ポイントをリセットする、*キャンセル*ルーチンを**NULL** IRP にします。 ルーチンは、I/O IRP の入力を処理を開始できます。

ルーチンは、のエントリ ポイントをリセットする必要があります、*キャンセル*IRP 合格した場合、すぎる、Irp さらに処理するための日常的なその他のドライバーによってルーチンとそれらの Irp 保持されている取り消しできる状態にします。

キャンセル可能な状態では IRP を保持する任意の高度なドライバーをリセットする必要があります、*キャンセル*へのエントリ ポイント**NULL** IRP が使用してドライバーを次の下位に渡す前に**保留**.

### <a name="canceling-an-irp"></a>IRP のキャンセル

高度なドライバーを呼び出すことができます[ **IoCancelIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548338) IRP を割り当てられたを持ち、さらに下位レベルのドライバーで処理するため渡されるとします。 ただし、このようなドライバーがステータスの特定の IRP が完了することを想定することはできません\_下位のドライバーによって取り消されました。

### <a name="synchronization"></a>同期

ドライバーできます (またはその設計によって、必要があります)、Irp のキャンセル可能な状態を追跡するためにそのデバイスの拡張機能の追加の状態情報を維持します。 かどうか、この状態は、IRQL で実行されているドライバー ルーチンによって共有されます&lt;= ディスパッチ\_ドライバーに割り当てられた、初期化のスピン ロックでの共有データの保護レベル、します。

ドライバーの買収を管理する必要があり、システムのリリースはスピン ロックし、スピン ロックを慎重にキャンセルします。 最短の間隔のシステム キャンセル スピン ロックを保持する必要があります。 キャンセル可能な IRP をアクセスする前にこのようなドライバーを必ずチェックの戻り値[ **IoSetCancelRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549674)を決定するかどうか、*キャンセル*ルーチンが既にには実行している (またはが実行しようとしています)。できるようにする必要がありますので場合、*キャンセル*ルーチンが IRP を完了します。

これらの他のルーチンが ISR と共有状態へのアクセスを同期する必要がありますデバイス ドライバーがドライバーのさまざまなルーチンは、ISR と共有するキャンセル可能な Irp に関する状態情報を保持する場合 のみ、ドライバーによって提供される*SynchCritSection*ルーチンは、ISR マルチプロセッサの安全な方法で共有される状態情報にアクセスできます。

詳細については、次を参照してください。[同期手法](synchronization-techniques.md)します。

 

 




