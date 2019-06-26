---
title: IRP の完了
description: IRP の完了
ms.assetid: 3174b36c-feb5-497c-a6e4-0d070c658899
keywords:
- IRP ディスパッチ ルーチン WDK ファイル システム、Irp の完了
- WDK のファイル システムを要求する I/O の完了
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d96d1301bcb4ce22aaf78cc31cf48eb7adb32155
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363552"
---
# <a name="completing-the-irp"></a>IRP の完了


## <span id="ddk_handling_the_control_device_object_case_if"></span><span id="DDK_HANDLING_THE_CONTROL_DEVICE_OBJECT_CASE_IF"></span>


各ディスパッチ ルーチンに IRP のターゲット デバイスのオブジェクトへのポインターを受け取るその*デバイス オブジェクト*パラメーター。 フィルター ドライバーに制御デバイス オブジェクト (CDO) がある場合は、ディスパッチ ルーチンを確認する必要があるかどうか、*デバイス オブジェクト*IRP の処理を実行する前に、ポインターが、フィルター ドライバーの CDO を指します。

ファイル システム フィルター ドライバーは、具体的には、CDO に送信されるすべての I/O 操作をサポートする必要はありません。 (一般的にサポートされている操作の詳細については、次を参照してください[フィルター ドライバーの制御デバイス オブジェクト](the-filter-driver-s-control-device-object.md)。)。ただし、CDO に送信されるすべての IRP を完了する必要があります。

*完了*IRP、ディスパッチ ルーチンをする必要がありますすべての実行、次の手順。

1.  設定**Irp -&gt;IoStatus.Status** NTSTATUS の適切な値にします。

2.  呼び出す[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) IRP を I/O マネージャーに戻ります。

3.  呼び出し元には、手順 1 と同じ状態の値を返します。

IRP の完了は「成功」または「失敗」IRP と呼ばれるをことがあります。

-   *成功*IRP が成功または状態などの情報の NTSTATUS 値を使用することを意味\_成功します。

-   *失敗*IRP の状態などのエラーまたは警告の NTSTATUS 値を使用することを意味\_無効な\_デバイス\_要求または状態\_バッファー\_オーバーフローします。

NTSTATUS の値は ntstatus.h に定義されます。 これらの値は 4 つのカテゴリに分類されます。 成功すると、情報、警告、およびエラー。 詳細については、次を参照してください。 [NTSTATUS 値を使用して](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-ntstatus-values)します。

**注**  が状態\_PENDING は成功 NTSTATUS 値、状態が IRP を完了すると、プログラミング エラー\_保留します。

 

 

 




