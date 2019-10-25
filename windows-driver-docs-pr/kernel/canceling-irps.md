---
title: IRP のキャンセル
description: IRP のキャンセル
ms.assetid: da199435-f6c3-44f4-b1ed-0280f39ee452
keywords:
- Irp WDK カーネル、キャンセル
- Irp の取り消し
- キャンセルルーチン
- ユーザーによって取り消された i/o 要求 (WDK カーネル)
- Irp WDK カーネルを完了し、Irp をキャンセルする
- 未処理の IRP キャンセル WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 717abfac19a7ed0564344f56e71a847581a745e1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828548"
---
# <a name="canceling-irps"></a>IRP のキャンセル





Irp が無期限にキューに置かれている可能性のあるドライバー (ユーザーが以前に送信した i/o 要求をキャンセルできるようにするため) には、ユーザーがキャンセルした i/o 要求を完了するために1つ以上の[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンが必要です。 たとえば、キーボード、マウス、パラレル、シリアル、およびサウンドデバイスドライバー (またはそれらに重なっているドライバー) とファイルシステムドライバーに*キャンセル*ルーチンが含まれている必要があります。

Microsoft Windows XP 以降のオペレーティングシステムのドライバーでは、独自の*キャンセル*ルーチンを実装するのではなく、[キャンセルセーフな IRP キュー](cancel-safe-irp-queues.md)を使用できます。

"IRP をキャンセルする" とは、システムの整合性を維持したまま、できるだけ早く IRP を完了することを意味します。 IRP の完了に関する一般的な説明については、「 [irp の完了](completing-irps.md)」を参照してください。

システムまたはドライバーが[**Iocancelirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)を呼び出すと、キャンセルプロセスが開始されます。 このルーチンは、まだ完全に完了していないスレッドに関連付けられている各 IRP に対して呼び出されます。 I/o 要求を開始したスレッドが終了した場合、システムは未処理の Irp をキャンセルします。 ドライバーは、自分が作成した Irp だけを取り消すことができます (「[下位レベルのドライバーの irp の作成](creating-irps-for-lower-level-drivers.md)」を参照してください)。

IRP が5分以内に完了しなかった場合、i/o マネージャーは IRP がタイムアウトしたと見なします。このような Irp はスレッドとの関連付けが解除され、現在 IRP を所有しているデバイスに対してエラーが記録されます。 ドライバーで完了するまでに時間がかかる可能性のある要求はキャンセル可能であることを確認してください。 長い要求がキャンセル可能であることを確認するには、[キャンセルセーフの IRP キュー](cancel-safe-irp-queues.md)または[カーネルモードドライバーのフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/design-guide)を使用します。これにより、ドライバーの開発者からのキャンセルが抽象化されます。

ここでは、次のトピックについて説明します。

[キャンセルルーチンの概要](introduction-to-cancel-routines.md)

[キャンセルルーチンの登録](registering-a-cancel-routine.md)

[IRP の取り消しを同期しています](synchronizing-irp-cancellation.md)

[キャンセルルーチンの実装](implementing-a-cancel-routine.md)

[Irp をキャンセルする場合の考慮事項](points-to-consider-when-canceling-irps.md)

 

 




