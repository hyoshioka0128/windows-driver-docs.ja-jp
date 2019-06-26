---
title: ドライバーによって管理される IRP キュー
description: ドライバーによって管理される IRP キュー
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
ms.openlocfilehash: a459bcbbf3193b1f5203f1d1b60a4d6126ed5966
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384961"
---
# <a name="driver-managed-irp-queues"></a>ドライバーによって管理される IRP キュー





ファイル システム ドライバーを除いては、I/O マネージャーは、(キューの Irp) のデバイスのキュー オブジェクトをドライバーを作成する各デバイス オブジェクトに関連付けます。

対象のデバイス オブジェクトのデバイスの I/O が要求されるたびに、Irp を保持する、関連付けられているデバイスのキューを使用する I/O マネージャーのサポート ルーチンにドライバーよりも高速はほとんどのデバイス ドライバーの呼び出しは、完了するまでそれらを処理できます。 この手法で Irp がドライバーが提供するキューに[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチン。

良好なパフォーマンスは、中間のほとんどのドライバーだけを渡す Irp 下位のドライバーに、それらが高速ので、中間のドライバーがほとんどない、それぞれのデバイス オブジェクトに関連付けられているデバイスのキューを使用します。

ただし、1 つまたは複数のデバイスのキュー、インタロックされたキュー、またはキャンセルの安全なキューを明示的に設定して Irp の内部キューを管理するためのドライバーを設計できます。 このアプローチは、ドライバーは、I/O 操作と重複するデバイスを制御する場合に特に役立ちますできます。 このようなデバイスの場合は 1 つのキューのみを使用して、同じターゲット デバイス オブジェクトの 2 つ以上の Irp の同時処理を管理しにくいことができます。

キャンセルの安全な IRP のキューのフレームワークを使用することを内部キューを作成する最も簡単な方法です。 ドライバーは、任意のキュー メカニズムを実装できます。 使用することができますし、 [ **IoCsqInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinitialize) IRP の挿入と削除だけでなくロックと、キューをロック解除を処理するコールバック ルーチンのセットを登録します。 キャンセルの安全な IRP のキューのフレームワークを提供します、 [ **IoCsqInsertIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirp)、 [ **IoCsqRemoveIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqremoveirp)、および[ **IoCsqRemoveNextIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqremovenextirp)自動的に安全に挿入したり、ドライバーのキューから Irp を削除したり、コールバック ルーチンを使用するルーチン。 システムでは、取り消された任意の Irp を安全に削除するのにユーザー コールバック ルーチンも使用します。

一連の異種の物理デバイスのデバイス コント ローラーのドライバーで Irp の補足のキューを設定することをも可能性があります。 たとえば、SCSI ポート ドライバーは、内部キューのデバイスのキュー オブジェクトを使用します。 このドライバーには、 *StartIo*ルーチンとデバイスのセットは、補足のキューと同じようにオブジェクトをキューでだけでなく、デバイス オブジェクトに関連付けられているデバイスのキューには、HBA を表すが作成されます。 SCSI ポート ドライバーでは、その補足デバイス キューを使用して、Irp HBA 制御 SCSI バス上の特定の論理ユニットのバインドを保持します。

システムのフロッピー コント ローラー ドライバーがないドライバーの例に示します*StartIo*ルーチン、インタロックされたキューを使用しています。 このドライバーはダブルリンク インタロックされたキューにし、元のドライバーとそのデバイス専用のスレッドを挿入および Irp の削除を設定します。

カーネルは、デバイスのキュー オブジェクトの種類を定義します。 経営陣の支持コンポーネントは、挿入およびインタロックされたキューで Irp を削除するためのルーチンを提供します。 Windows XP および Windows の以降のバージョン用のドライバーを使用できる[キャンセル セーフ IRP キュー](cancel-safe-irp-queues.md) IRP のキューを処理します。

次のセクションでは、デバイスのキュー、インタロックされたキュー、およびキャンセルの安全なキューを使用する方法について説明します。

[セットアップとデバイスのキューの使用](setting-up-and-using-device-queues.md)

[デバイスのキューを管理します。](managing-device-queues.md)

[設定して、インタロックされたキューを使用します。](setting-up-and-using-interlocked-queues.md)

[ドライバーが作成したスレッドにインタロックされたキューを管理します。](managing-interlocked-queues-with-a-driver-created-thread.md)

[キャンセルの安全な IRP のキュー](cancel-safe-irp-queues.md)

 

 




