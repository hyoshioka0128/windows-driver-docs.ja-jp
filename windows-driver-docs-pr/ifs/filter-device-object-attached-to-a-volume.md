---
title: ボリュームにアタッチされるフィルター デバイス オブジェクト
description: ボリュームにアタッチされるフィルター デバイス オブジェクト
ms.assetid: cf152065-fc03-4f5f-b65b-13a76e83d745
keywords:
- デバイス オブジェクトの WDK ファイル システム フィルターをかける
- デバイス オブジェクトの I/O 要求ドライバー WDK のファイル システムをフィルター処理します。
- ファイル システム フィルター ドライバー WDK、デバイス オブジェクトの I/O 要求
- WDK のボリューム ファイル システム、デバイス オブジェクトの I/O 要求
- デバイス オブジェクトの I/O 要求の WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e90725415de436bfec0c21f6f19ec61630c8c5d8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369250"
---
# <a name="filter-device-object-attached-to-a-volume"></a>ボリュームにアタッチされるフィルター デバイス オブジェクト


## <span id="ddk_a_filter_device_object_attached_to_a_volume_if"></span><span id="DDK_A_FILTER_DEVICE_OBJECT_ATTACHED_TO_A_VOLUME_IF"></span>


ボリュームをフィルターするには、フィルター ドライバーは、フィルター デバイス オブジェクトを作成し、ボリュームのボリュームのデバイス オブジェクトの上にアタッチします。

### <a name="span-idtypesofiorequeststhataresenttoavolumespanspan-idtypesofiorequeststhataresenttoavolumespantypes-of-io-requests-that-are-sent-to-a-volume"></a><span id="types_of_i_o_requests_that_are_sent_to_a_volume"></span><span id="TYPES_OF_I_O_REQUESTS_THAT_ARE_SENT_TO_A_VOLUME"></span>ボリュームに送信される I/O 要求の種類

ボリューム上に関連付けられているフィルター デバイス オブジェクトは、次の種類の I/O 要求を受信する概してできます。

[**IRP\_MJ\_クリーンアップ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-cleanup)

[**IRP\_MJ\_CLOSE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-close)

[**IRP\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)

[**IRP\_MJ\_DEVICE\_CONTROL**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-device-control)

[**IRP\_MJ\_ディレクトリ\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-directory-control)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)

[**IRP\_MJ\_フラッシュ\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-flush-buffers)

[**IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-internal-device-control)

[**IRP\_MJ\_ロック\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-lock-control)

[**IRP\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-pnp)

[**IRP\_MJ\_クエリ\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-ea)

[**IRP\_MJ\_クエリ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-information)

[**IRP\_MJ\_クエリ\_クォータ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-quota)

[**IRP\_MJ\_QUERY\_SECURITY**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-security)

[**IRP\_MJ\_クエリ\_ボリューム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-volume-information)

[**IRP\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-read)

[**IRP\_MJ\_SET\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-ea)

[**IRP\_MJ\_SET\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-information)

[**IRP\_MJ\_SET\_QUOTA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-quota)

[**IRP\_MJ\_SET\_SECURITY**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-security)

[**IRP\_MJ\_設定\_ボリューム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-volume-information)

[**IRP\_MJ\_シャット ダウン**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-shutdown)

[**IRP\_MJ\_WRITE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-write)

**FastIoCheckIfPossible**

**FastIoDetachDevice**

**FastIoDeviceControl**

**FastIoLock**

**FastIoQueryBasicInfo**

**FastIoQueryNetworkOpenInfo**

**FastIoQueryOpen**

**FastIoQueryStandardInfo**

**FastIoRead**

**FastIoReadCompressed**

**FastIoUnlockAll**

**FastIoUnlockAllByKey**

**FastIoUnlockSingle**

**FastIoWrite**

**FastIoWriteCompressed**

**MdlRead**

**MdlReadComplete**

**MdlReadCompleteCompressed**

**MdlWriteComplete**

**MdlWriteCompleteCompressed**

**PrepareMdlWrite**

ドライバー スタックで、次の下位ドライバーにすべての認識できない、または望ましくない Irp を渡すには、既定では、ボリュームに接続されている、ファイル システム フィルター デバイス オブジェクトが必要です。 さらに、それらを実装する必要があります**FastIoDetachDevice**します。

**注**   Microsoft Windows XP にし、後で、次の高速な I/O コールバック ルーチンが廃止され、ファイル システム フィルター ドライバーでは使用できません。**AcquireForCcFlush**

**AcquireFileForNtCreateSection**

**AcquireForModWrite**

**ReleaseForCcFlush**

**ReleaseFileForNtCreateSection**

**ReleaseForModWrite**

詳細については、参照のエントリを参照してください。 [ **FsRtlRegisterFileSystemFilterCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)します。

 

 

 




