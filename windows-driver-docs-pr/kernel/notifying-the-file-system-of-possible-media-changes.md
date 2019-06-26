---
title: メディア変更の可能性に関するファイル システムへの通知
description: メディア変更の可能性に関するファイル システムへの通知
ms.assetid: b1956370-ec9c-4a43-90a8-12705d28e314
keywords:
- WDK カーネルをリムーバブル メディア、メディアの変更の通知
- WDK のリムーバブル メディアの通知
- 変更通知 WDK リムーバブル メディアをメディア
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba681783d64fb52d2f0921d77bfad2a421295539
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354992"
---
# <a name="notifying-the-file-system-of-possible-media-changes"></a>メディア変更の可能性に関するファイル システムへの通知





リムーバブル メディア デバイス ドライバーでは、によって表されるデバイスのメディアが変更されていないことを確認する必要があります、**デバイス オブジェクト**(IRP が送信されるすべてのドライバーのルーチンへの入力)、ドライバーが転送を要求する IRP を処理するたびに/からメディアまたはデバイスの I/O 制御操作は、メディアに影響します。 変更されたメディアを確認する最適な可能なタイミングは、物理デバイスは、これらの状態変更について、ドライバーを常に通知された場合に、いいえ-メディア-現在の状態からメディア存在状態への移行後にだけです。

その物理デバイスでは、ドライバーは、I/O 操作を開始する前に、メディアの状態が変更された可能性を示している場合、または操作中に、ドライバー、次の操作する必要があります。

1.  VPB をチェックして、ボリュームがマウントされていることを確認\_でマウントされたフラグ、 *VPB*します。 (ドライバーは設定しないで、ボリュームがマウントされていない場合\_確認\_ボリューム ビット。 ドライバーを設定する必要があります**IoStatus.Status**ステータス\_IO\_デバイス\_セットのエラー、 **IoStatus.Information**をゼロにして呼び出す[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) IRP にします)。

2.  設定、**フラグ**で、**デバイス オブジェクト**Or で**フラグ**か\_確認\_ボリューム。

3.  設定、 **IoStatus** IRP が、次のブロックします。
    -   **ステータス**状態に設定\_確認\_必要な作業
    -   **情報**を 0 に設定

4.  任意の IRP を完了する前に、 **IoStatus**をブロック、**状態**フィールドは、状態に設定されていない\_成功すると、ドライバーが呼び出す必要があります[ **IoIsErrorUserInduced**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioiserroruserinduced)、ブール値を返す**TRUE** 、次のいずれかの**状態**値。

    -   ステータス\_確認\_必要な作業
    -   ステータス\_いいえ\_メディア\_IN\_デバイス
    -   ステータス\_間違った\_ボリューム
    -   ステータス\_"認識されません"\_メディア
    -   ステータス\_メディア\_書き込み\_保護
    -   ステータス\_IO\_タイムアウト
    -   ステータス\_デバイス\_いない\_準備完了

    場合**IoIsErrorUserInduced**返します**TRUE**、ドライバーを呼び出す必要があります[ **IoSetHardErrorOrVerifyDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iosetharderrororverifydevice) FSD ダイアログ ボックスを開くことができます。ユーザーに、正しいメディアを指定、元の要求を再試行してください。 または、要求された操作をキャンセルを選択できます。

 

 




