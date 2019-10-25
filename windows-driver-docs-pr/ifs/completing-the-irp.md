---
title: IRP の完了
description: IRP の完了
ms.assetid: 3174b36c-feb5-497c-a6e4-0d070c658899
keywords:
- IRP ディスパッチルーチン WDK ファイルシステム、Irp の完了
- i/o 要求の完了 (WDK ファイルシステム)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7344d1d44aa4300a72dabc15da44ccec319abf6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841466"
---
# <a name="completing-the-irp"></a>IRP の完了


## <span id="ddk_handling_the_control_device_object_case_if"></span><span id="DDK_HANDLING_THE_CONTROL_DEVICE_OBJECT_CASE_IF"></span>


各ディスパッチルーチンは、 *DeviceObject*パラメーターで IRP のターゲットデバイスオブジェクトへのポインターを受け取ります。 フィルタードライバーにコントロールデバイスオブジェクト (CDO) がある場合、ディスパッチルーチンは、IRP で処理を実行する前に、 *DeviceObject*ポインターがフィルタードライバーの cdo を指しているかどうかを確認する必要があります。

ファイルシステムフィルタードライバーは、CDO に特に送信される i/o 操作をサポートするためには必要ありません。 (一般的にサポートされる操作の詳細については、[フィルタードライバーのコントロールデバイスオブジェクト](the-filter-driver-s-control-device-object.md)に関する説明を参照してください)。ただし、CDO は、送信されるすべての IRP を完了する必要があります。

IRP を*完了*するには、ディスパッチルーチンで次のすべての手順を実行する必要があります。

1.  **Irp&gt;IoStatus. status**を適切な NTSTATUS 値に設定します。

2.  [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して、IRP を i/o マネージャーに返します。

3.  手順 1. と同じ状態値を呼び出し元に返します。

IRP の完了は、"成功" または "失敗" と呼ばれることもあります。

-   IRP を*成功*させるには、正常に完了したか、ステータス\_success などの情報の NTSTATUS 値を使用して IRP を完了します。

-   IRP がエラーまたは警告を使用して完了するために*失敗*する場合は\_無効\_デバイス\_の要求または状態\_バッファー\_オーバーフローします。

NTSTATUS 値は、ntstatus に定義されています。 これらの値は、成功、情報、警告、エラーの4つのカテゴリに分類されます。 詳細については、「 [NTSTATUS 値の使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-ntstatus-values)」を参照してください。

**注**   STATUS\_pending は成功した NTSTATUS 値ですが、状態\_保留中の IRP を完了するためのプログラミングエラーです。

 

 

 




