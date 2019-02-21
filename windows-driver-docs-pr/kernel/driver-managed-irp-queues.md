---
title: IRP のドライバー管理キュー
description: IRP のドライバー管理キュー
ms.assetid: b701e4aa-96ba-44af-96a5-b6cecf075bac
keywords:
- デバイスは、WDK の Irp でオブジェクトをキューします。
- Irp WDK カーネルでは、キュー
- キューの Irp
- Irp をデキューする.
- IRP キュー WDK カーネルの内部
- キャンセルの安全な IRP キュー WDK カーネル
- ドライバー管理 IRP キュー WDK のカーネル
- 補足の IRP キュー WDK カーネル
- インタロックされた IRP キュー WDK カーネル
- デバイスのキュー WDK Irp
- デバイスのキュー WDK Irp では、デバイスのキューについて
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9ebe8a4e657ff53dd6456bdfa98266798a687e0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539626"
---
# <a name="driver-managed-irp-queues"></a>IRP のドライバー管理キュー





ファイル システム ドライバーを除いては、I/O マネージャーは、(キューの Irp) のデバイスのキュー オブジェクトをドライバーを作成する各デバイス オブジェクトに関連付けます。

対象のデバイス オブジェクトのデバイスの I/O が要求されるたびに、Irp を保持する、関連付けられているデバイスのキューを使用する I/O マネージャーのサポート ルーチンにドライバーよりも高速はほとんどのデバイス ドライバーの呼び出しは、完了するまでそれらを処理できます。 この手法で Irp がドライバーが提供するキューに[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチン。

良好なパフォーマンスは、中間のほとんどのドライバーだけを渡す Irp 下位のドライバーに、それらが高速ので、中間のドライバーがほとんどない、それぞれのデバイス オブジェクトに関連付けられているデバイスのキューを使用します。

ただし、1 つまたは複数のデバイスのキュー、インタロックされたキュー、またはキャンセルの安全なキューを明示的に設定して Irp の内部キューを管理するためのドライバーを設計できます。 このアプローチは、ドライバーは、I/O 操作と重複するデバイスを制御する場合に特に役立ちますできます。 このようなデバイスの場合は 1 つのキューのみを使用して、同じターゲット デバイス オブジェクトの 2 つ以上の Irp の同時処理を管理しにくいことができます。

キャンセルの安全な IRP のキューのフレームワークを使用することを内部キューを作成する最も簡単な方法です。 ドライバーは、任意のキュー メカニズムを実装できます。 使用することができますし、 [ **IoCsqInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff549054) IRP の挿入と削除だけでなくロックと、キューをロック解除を処理するコールバック ルーチンのセットを登録します。 キャンセルの安全な IRP のキューのフレームワークを提供します、 [ **IoCsqInsertIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549066)、 [ **IoCsqRemoveIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549070)、および[ **IoCsqRemoveNextIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549072)自動的に安全に挿入したり、ドライバーのキューから Irp を削除したり、コールバック ルーチンを使用するルーチン。 システムでは、取り消された任意の Irp を安全に削除するのにユーザー コールバック ルーチンも使用します。

一連の異種の物理デバイスのデバイス コント ローラーのドライバーで Irp の補足のキューを設定することをも可能性があります。 たとえば、SCSI ポート ドライバーは、内部キューのデバイスのキュー オブジェクトを使用します。 このドライバーには、 *StartIo*ルーチンとデバイスのセットは、補足のキューと同じようにオブジェクトをキューでだけでなく、デバイス オブジェクトに関連付けられているデバイスのキューには、HBA を表すが作成されます。 SCSI ポート ドライバーでは、その補足デバイス キューを使用して、Irp HBA 制御 SCSI バス上の特定の論理ユニットのバインドを保持します。

システムのフロッピー コント ローラー ドライバーがないドライバーの例に示します*StartIo*ルーチン、インタロックされたキューを使用しています。 このドライバーはダブルリンク インタロックされたキューにし、元のドライバーとそのデバイス専用のスレッドを挿入および Irp の削除を設定します。

カーネルは、デバイスのキュー オブジェクトの種類を定義します。 経営陣の支持コンポーネントは、挿入およびインタロックされたキューで Irp を削除するためのルーチンを提供します。 Windows XP および Windows の以降のバージョン用のドライバーを使用できる[キャンセル セーフ IRP キュー](cancel-safe-irp-queues.md) IRP のキューを処理します。

次のセクションでは、デバイスのキュー、インタロックされたキュー、およびキャンセルの安全なキューを使用する方法について説明します。

[セットアップとデバイスのキューの使用](setting-up-and-using-device-queues.md)

[デバイスのキューを管理します。](managing-device-queues.md)

[設定して、インタロックされたキューを使用します。](setting-up-and-using-interlocked-queues.md)

[ドライバーが作成したスレッドにインタロックされたキューを管理します。](managing-interlocked-queues-with-a-driver-created-thread.md)

[キャンセルの安全な IRP のキュー](cancel-safe-irp-queues.md)

 

 




