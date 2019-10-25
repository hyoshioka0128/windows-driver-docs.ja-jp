---
title: 記憶域クラス ドライバーの RetryRequest ルーチン
description: 記憶域クラス ドライバーの RetryRequest ルーチン
ms.assetid: de1eea7d-88db-444c-a9f7-462ad4a5df27
keywords:
- RetryRequest
- WDK ストレージの再試行要求
- エラー WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5991d4d6e6dc7aff5da2a9d5ccbad1836ed1a0d4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841608"
---
# <a name="storage-class-drivers-retryrequest-routine"></a>記憶域クラス ドライバーの RetryRequest ルーチン


## <span id="ddk_storage_class_drivers_retryrequest_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_RETRYREQUEST_ROUTINE_KG"></span>


バスパリティエラー、選択されたタイムアウト、ターゲット/コントローラービジーエラーなど、バス上のデータの転送を含むデバイスエラーが発生した場合、基になるストレージポートドライバーは、要求を再試行します。 再試行の試行が失敗した場合、ストレージポートドライバーは、適切なエラーで要求を完了し、i/o エラーもログに記録します。

ストレージクラスドライバーは、上記のいずれかのエラーが原因でポートドライバーが既に失敗したという要求の再試行を試行しません。

ストレージクラスドライバーは、デバイス固有のエラー、ターゲット/コントローラーのビジー状態、バスのリセット、または要求のタイムアウトによって失敗した要求を再試行する役割を担います。 一般に、 *Retryrequest*ルーチンは、このような IRP を次の下位のドライバーに再送信し、ポートドライバーの LU 固有のキューの先頭に SRB を配置するように指示することができます。

特に、 *Retryrequest*ルーチンは次の処理を実行する必要があります。

1.  部分転送要求の開始アドレスと長さに正しい値が設定されていることを確認します。

2.  SRB の**Srbstatus**メンバーと**ScsiStatus**メンバーをゼロにします。

3.  デバイスに必要な**Srbflags**メンバーを設定します。

4.  「ストレージクラスドライバーの[SplitTransferRequest ルーチン](storage-class-driver-s-splittransferrequest-routine.md)による[ストレージクラスドライバーのディスパッチルーチン](storage-class-driver-s-dispatch-routines.md)」で既に説明したように、IRP でポートドライバーの i/o スタックの場所を設定します。

5.  Irp に対して[**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出します。これは、irp が戻る前に、ドライバーの[**IOCOMPLETION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンが SRB を解放する必要があるためです。 *Iocompletion*ルーチンでは、要求を複数回再試行したり、ドライバーの*解釈 Requestsense*または*releasequeue*ルーチンを呼び出したりすることが必要になる場合もあります。

6.  [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を使用して、要求を次の下位のドライバーに渡します。

 

 




