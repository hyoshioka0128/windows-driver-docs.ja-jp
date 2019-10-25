---
title: メディア変更の可能性に関するファイル システムへの通知
description: メディア変更の可能性に関するファイル システムへの通知
ms.assetid: b1956370-ec9c-4a43-90a8-12705d28e314
keywords:
- リムーバブルメディアの WDK カーネル、メディアの変更の通知
- 通知 WDK リムーバブルメディア
- メディア変更通知 WDK リムーバブルメディア
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6531c7973498d440afac39ba5971a496c04ee14e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827818"
---
# <a name="notifying-the-file-system-of-possible-media-changes"></a>メディア変更の可能性に関するファイル システムへの通知





リムーバブルメディアデバイスドライバーは、メディアまたはからの転送を要求する IRP をドライバーが処理するたびに、 **DeviceObject**によって表されるデバイスのメディアが変更されていないことを確認する必要があります (irp が送信されるすべてのドライバールーチンへの入力)。メディアに影響を与えるデバイス i/o 制御操作。 変更されたメディアを確認する最善の方法は、物理デバイスがこれらの状態の変更について常にドライバーに通知する場合は、メディアが存在しない状態からメディアが存在する状態に移行した直後です。

ドライバーが i/o 操作を開始する前、または操作中に、メディアの状態が変更された可能性がある場合、ドライバーは次の操作を行う必要があります。

1.  Vpb の VPB\_マウントフラグをチェックして、ボリュームがマウントされていることを確認*します。* (ボリュームがマウントされていない場合、ドライバーは DO\_VERIFY\_ボリュームビットを設定しないようにする必要があります。 ドライバーは**Iostatus. status**を STATUS\_IO\_デバイス\_エラーに設定し、 **Iostatus. 情報**を0に設定し、IRP で[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出します。

2.  **DeviceObject**でフラグを設定するには **、\_** ボリュームを確認\_で**フラグ**を設定します。

3.  IRP の**Iostatus**ブロックを次のように設定します。
    -   **状態を状態に設定\_** 確認\_必要
    -   0に設定される**情報**

4.  **Iostatus**ブロックで IRP を完了する前に、 **status**フィールドが status\_SUCCESS に設定されていない場合、ドライバーは[**IoIsErrorUserInduced**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioiserroruserinduced)を呼び出す必要があります。これにより、次のいずれかの状態に対してブール値の**TRUE**が返されます。値:

    -   状態\_確認\_必要
    -   ステータス\_\_デバイスに\_メディア\_がありません
    -   状態\_\_ボリュームが間違っています
    -   ステータス\_認識されない\_メディア
    -   状態\_メディア\_書き込み\_保護されている
    -   状態\_IO\_タイムアウト
    -   状態\_デバイス\_準備ができていません\_

    **IoIsErrorUserInduced**が**TRUE**を返す場合、ドライバーは[**IoSetHardErrorOrVerifyDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iosetharderrororverifydevice)を呼び出す必要があります。これにより、FSD はユーザーに対してダイアログボックスを開き、正しいメディアを指定したり、元の要求を再試行したり、要求されたをキャンセルしたりできます。運用.

 

 




