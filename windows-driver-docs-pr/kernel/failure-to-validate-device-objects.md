---
title: デバイス オブジェクトの検証失敗
description: デバイス オブジェクトの検証失敗
ms.assetid: aa4abc20-0b87-44d7-8987-a5b2be397bb1
keywords:
- 信頼性 WDK カーネル、デバイスオブジェクトの検証
- デバイスオブジェクト WDK カーネル、検証エラー
- 検証エラー (WDK カーネル)
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca192ba18a9903cc80f8378e16526208bee01909
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836715"
---
# <a name="failure-to-validate-device-objects"></a>デバイス オブジェクトの検証失敗





多くのドライバーでは、 [**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)を呼び出すことによって、複数の種類のデバイスオブジェクトを作成します。 ドライバーによっては、ドライバーが FDO を作成する前でも、ドライバーとの通信を可能にするために、 **Driverentry**ルーチンにコントロールデバイスオブジェクトが作成されます。 たとえば、ファイルシステムドライバーは、ファイルシステムの通知を**IoRegisterFileSystem**を使用してファイルシステムとして登録するときに、ファイルシステムの通知を処理するデバイスオブジェクトを作成します。

ドライバーは、作成したデバイスオブジェクトに対して要求を[**作成\_、IRP\_MJ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)の準備ができている必要があります。 要求が成功の状態で完了した後、ドライバーは、作成されたファイルオブジェクトに対してユーザーがアクセスできる i/o 要求を受け取ることを想定します。 そのため、複数のデバイスオブジェクトを作成するすべてのドライバーは、i/o 要求ごとに指定されているデバイスオブジェクトを確認する必要があります。

たとえば、ドライバーが[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)にコントロールデバイスオブジェクト全体を作成し、その[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンに別のデバイスオブジェクトセットを作成したとします。 *AddDevice*ルーチンが下位レベルのドライバーに関する情報を使用してデバイス拡張機能を初期化するとしますが、コントロールデバイスオブジェクトにはこの情報が含まれていません。 この場合、受信した各デバイスオブジェクトを確認するために、すべてのディスパッチルーチンに注意する必要があります。 それ以外の場合、デバイス拡張機能の情報を使用しようとすると、ドライバーがクラッシュする可能性があります。

 

 




