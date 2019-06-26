---
title: キャンセル ルーチンの実装
description: キャンセル ルーチンの実装
ms.assetid: 243b623b-317c-4084-a753-940c91c4cc50
keywords:
- Irp、ガイドラインのキャンセル
- キャンセル ルーチン、ガイドライン
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9c57afb0e5099cd3591b17bd8de241cb77c463a1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365814"
---
# <a name="implementing-a-cancel-routine"></a>キャンセル ルーチンの実装





I/O マネージャーでは、ドライバーによって提供される[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)ルーチンをキャンセルできる IRP の入力と*デバイス オブジェクト*I/O に対してターゲット デバイスを表すポインター要求。

IRP はいずれかになりますドライバーの[ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンがキューに入って、ユーザーが現在の Win32 アプリケーションが閉じられると同様。 IRP 場合もありますより高度なドライバーを明示的に取り消された場合、基になるデバイスの性質によっては 1 つ。

ときに、*キャンセル*ルーチンを呼び出すと、入力の IRP 場合によっては既に、 **CurrentIrp**ターゲット デバイスのオブジェクトまたはが既にである場合は、ターゲット デバイス オブジェクトに関連付けられているデバイスのキューでドライバー[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチン。 ドライバーがにない場合*StartIo* 、日常的な IRP あります Irp のドライバー管理の内部キューでときにその*キャンセル*ルーチンが呼び出されます。 I/O マネージャーの呼び出しの前にいずれの場合も、*キャンセル*受信 IRP の日常的な I/O マネージャーの設定、**キャンセル**メンバーには、この IRP の**TRUE** の設定と**CancelRoutine** IRP をメンバー **NULL**します。

*キャンセル*Irp が関連付けられている IRP が通話を担当マスターの日常的な[ **IoCancelIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocancelirp) Irp を関連付けられているものをキャンセルします。

すべて*キャンセル*ルーチンが次のガイドラインに従う必要があります。

-   呼び出す[ **IoReleaseCancelSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))システムのキャンセル スピン ロックを解放します。

-   I/O 状態ブロックの設定**状態**メンバーの状態を\_取り消し済み、およびセットの**情報**メンバーをゼロにします。

-   指定した IRP を呼び出して完了[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)します。

-   *キャンセル*ルーチンが保持されているシステム キャンセル スピン ロックで常に呼び出されると、このルーチンを呼び出してはならない[ **IoAcquireCancelSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85)) を呼び出さない限り、**IoReleaseCancelSpinLock**最初。

-   A*キャンセル*制御が戻ったときに、ルーチンでシステム キャンセル スピン ロックする保持ことはできません。 つまり、すべて*キャンセル*ルーチンを呼び出す必要があります**IoReleaseCancelSpinLock**を少なくとも 1 回制御を返す前にします。

-   呼び出す場合**IoAcquireCancelSpinLock**、*キャンセル*ルーチンは、相互の呼び出しを行う必要があります**IoReleaseCancelSpinLock**可能な限り早くします。

-   呼び出さない[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) IRP スピン ロックを保持しているときに使用します。 スピン ロックを保持しているときに IRP の完了を試みると、デッドロックが生じる場合があります。


 

 




