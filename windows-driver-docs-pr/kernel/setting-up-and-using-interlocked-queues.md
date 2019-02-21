---
title: 設定して、インタロックされたキューを使用します。
description: 設定して、インタロックされたキューを使用します。
ms.assetid: af44a4c0-5aa7-40aa-b511-df95c9bfe9bb
keywords:
- インタロックされた IRP キュー WDK カーネル
- ダブルリンク Irp WDK カーネル
- WDK Irp ドライバー専用のスレッド
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bea2e7ebbf5870f7c5e65bedea3fa7b2a867430
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531637"
---
# <a name="setting-up-and-using-interlocked-queues"></a>設定して、インタロックされたキューを使用します。





新しいドライバーを使用する必要があります、[キャンセル セーフ IRP キュー](cancel-safe-irp-queues.md)メソッドのこのセクションで概説した方が優先的フレームワーク。

デバイス専用のスレッドでのドライバーまたは fsd に対して表示される、ほとんどのシステムなどの実行ワーカー スレッドを使用するドライバーは、最も可能性の高いキューを管理する独自ランタイム内部 Irp のインタロックされたキューにドライバーの種類です。 WDM ドライバーなど、すべての PnP ドライバーもする必要があります内部キューに配置特定の Irp PnP および電源の状態遷移中にします。

これらのドライバーは、通常、ダブルリンク インタロックされたキューを設定すべての IRP には型のメンバーが含まれています[**一覧\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff554296)が現在保持している Irp を二重にリンクするドライバーを使用できます。 ドライバーは、シングル リンク インタロックされたキューを設定する場合、再試行の Irp を入れることはできません。

### <a href="" id="ddk-using-an-interlocked-queue-kg"></a>

ドライバーは、デバイスの初期化時、インタロックされたキューを設定する必要があります。 次の図は、インタロックされたキューを二重にリンクされた、サポート ルーチン ドライバーは、このようなキュー、および一連のセットアップを呼び出す必要があります**ExInterlocked * Xxx*** ルーチンに Irp の挿入およびから Irp を削除するドライバーを呼び出すことができます、キューです。

![インタロックされたキューを使用して説明する図](images/3intlokq.png)

この図に示すようにドライバーをする必要がありますストレージを提供、キュー自体と、次のダブルリンク インタロックされたキューを設定するには。

-   ドライバーを呼び出す必要があります executive スピン ロックを[ **KeInitializeSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff552160)を初期化します。 ドライバーがスピン ロックを初期化するのには、そのデバイス オブジェクトのデバイスの拡張機能を設定するときに通常は、その[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチン。

-   呼び出すことによって、ドライバーを初期化する必要がありますキューのリストの先頭[ **InitializeListHead**](https://msdn.microsoft.com/library/windows/hardware/ff547799)します。

ダブルリンク インタロックされたキューを使用するほとんどのドライバーでは、デバイスのドライバーが作成したオブジェクトのデバイスの拡張機能に必要なストレージを提供します。 キューおよび executive スピン ロックに代わりに、コント ローラーの拡張機能にできます (ドライバーで使用する場合、[コント ローラー オブジェクト](using-controller-objects.md)) またはドライバーによって割り当てられた非ページ プール。

ドライバーでは、I/O 要求を受け付けて、中にそのキューの IRP が挿入場合、次のサポート ルーチンのいずれかを呼び出すことによって、 *ListHead*の種類は**一覧\_エントリ**ように、前の図。

[**ExInterlockedInsertTailList** ](https://msdn.microsoft.com/library/windows/hardware/ff545402) IRP をキューの末尾に配置するには

[**ExInterlockedInsertHeadList** ](https://msdn.microsoft.com/library/windows/hardware/ff545397) IRP をキューの先頭に配置します。 特定の要求を再試行する必要がある場合にのみ、ドライバーは、通常、このルーチンを呼び出します。

ドライバーは IRP にポインターを渡す必要があります (*ListEntry*)、および、 *ListHead*と executive スピン ロック (*ロック*) には既に初期化されて、これらの各ポインター**ExInterlockedInsert*Xxx*一覧**ルーチン。 ポインターのみ、 *ListHead*と*ロック*ドライバーを呼び出して、IRP をデキューするときに必要な[ **ExInterlockedRemoveHeadList** ](https://msdn.microsoft.com/library/windows/hardware/ff545427). デッドロックを防ぐためには、ドライバーする必要がありますいないを保持しているいずれかに渡される、ExecutiveSpinLock **ExInterlocked * Xxx*** ルーチン。

ドライバーが Irp を二重にリンクされた、キューに挿入し、マルチプロセッサ セーフ方式で実行中に以下よりまたは IRQL と等しく、ドライバー ルーチンから削除、インタロックされたキューが executive スピン ロックで保護されているために = ディスパッチ\_レベル。

型の listhead の位置を持つキュー**一覧\_エントリ**前の図に示すようはダブルリンク リストです。 1 つの種類の ListHead [ **SLIST\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff563810)シーケンスをシングル リンク リストです。 ドライバーの順序付けされたシングル リンクされたインタロックされたキューを呼び出して、ListHead を初期化します[ **ExInitializeSListHead**](https://msdn.microsoft.com/library/windows/hardware/ff545321)します。

I/O 操作を再試行しないドライバーを使用できます[ **ExInterlockedPushEntrySList** ](https://msdn.microsoft.com/library/windows/hardware/ff545422)と[ **ExInterlockedPopEntrySList** ](https://msdn.microsoft.com/library/windows/hardware/ff545414)にそのキュー Irp の内部シーケンスをシングル リンク インタロックされたキューでを管理します。 インタロックされたキューのこの型を使用する任意のドライバーには型の ListHead の常駐記憶域を提供する必要がありますもできます。 **SLIST\_ヘッダー** 、のように、ExecutiveSpinLock、[前図](#ddk-using-an-interlocked-queue-kg)します。 スピン ロックを初期化し、呼び出す前にそのキューを設定する必要があります、 **ExInterlockedPushEntrySList**そのキューに初期のエントリを挿入します。

詳細については、次を参照してください。[を管理するハードウェアの優先順位](managing-hardware-priorities.md)と[スピン ロック](spin-locks.md)します。 特定のサポート ルーチンの IRQL 要件、ルーチンのリファレンス ページを参照してください。

 

 




