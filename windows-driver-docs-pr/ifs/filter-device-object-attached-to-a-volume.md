---
title: ボリュームにアタッチされるフィルター デバイス オブジェクト
description: ボリュームにアタッチされるフィルター デバイス オブジェクト
ms.assetid: cf152065-fc03-4f5f-b65b-13a76e83d745
keywords:
- デバイスオブジェクトのフィルター WDK ファイルシステム
- フィルタードライバー WDK ファイルシステム、デバイスオブジェクトの i/o 要求
- ファイルシステムフィルタードライバー WDK、デバイスオブジェクト i/o 要求
- ボリューム WDK ファイルシステム、デバイスオブジェクト i/o 要求
- デバイスオブジェクト i/o 要求 (WDK ファイルシステム)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db370e568d32fff6a1cd5b220557ee2e14ac3dac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841400"
---
# <a name="filter-device-object-attached-to-a-volume"></a>ボリュームにアタッチされるフィルター デバイス オブジェクト


## <span id="ddk_a_filter_device_object_attached_to_a_volume_if"></span><span id="DDK_A_FILTER_DEVICE_OBJECT_ATTACHED_TO_A_VOLUME_IF"></span>


フィルタードライバーは、ボリュームをフィルター処理するために、フィルターデバイスオブジェクトを作成し、ボリュームのボリュームデバイスオブジェクトの上に接続します。

### <a name="span-idtypes_of_i_o_requests_that_are_sent_to_a_volumespanspan-idtypes_of_i_o_requests_that_are_sent_to_a_volumespantypes-of-io-requests-that-are-sent-to-a-volume"></a><span id="types_of_i_o_requests_that_are_sent_to_a_volume"></span><span id="TYPES_OF_I_O_REQUESTS_THAT_ARE_SENT_TO_A_VOLUME"></span>ボリュームに送信される i/o 要求の種類

ボリュームの上にアタッチされるフィルターデバイスオブジェクトは、通常、次の種類の i/o 要求を受け取ることがあります。

[**IRP\_MJ\_クリーンアップ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-cleanup)

[**IRP\_MJ\_閉じる**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-close)

[**IRP\_MJ\_作成**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)

[**IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-device-control)

[**IRP\_MJ\_DIRECTORY\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-directory-control)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)

[**IRP\_MJ\_フラッシュ\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-flush-buffers)

[**IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-internal-device-control)

[**IRP\_MJ\_ロック\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-lock-control)

[**IRP\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-pnp)

[**IRP\_MJ\_クエリ\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-ea)

[**IRP\_MJ\_クエリ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-information)

[**IRP\_MJ\_クエリ\_クォータ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-quota)

[**IRP\_MJ\_クエリ\_セキュリティ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-security)

[**IRP\_MJ\_クエリ\_ボリューム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-volume-information)

[**IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-read)

[**IRP\_MJ\_設定\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-ea)

[**IRP\_MJ\_設定\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-information)

[**IRP\_MJ\_設定\_クォータ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-quota)

[**IRP\_MJ\_設定\_セキュリティ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-security)

[**IRP\_MJ\_\_ボリューム\_情報の設定**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-volume-information)

[**IRP\_MJ\_シャットダウン**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-shutdown)

[**IRP\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-write)

**可能な場合**

**FastIoDetachDevice**

**Fa_ Odevicecontrol**

**Fa/Olock**

**Fa_ Oquerybasicinfo**

**Fa、Oquerynetworkopeninfo**

**Fa/Oqueryopen**

**Faの Oquerystandardinfo**

**FastIoRead**

**FastIoReadCompressed**

**Faと Ounlockall**

**FastIoUnlockAllByKey**

**Faと Ounlocksingle**

**高速**

**Fa/Owritecom押された状態**

**MdlRead**

**MdlReadComplete**

**MdlReadCompleteCompressed**

**MdlWriteComplete**

**MdlWriteCompleteCompressed**

**作成した Mdlwrite**

ボリュームにアタッチされているファイルシステムフィルターデバイスオブジェクトは、既定では、すべての認識されていない Irp または望ましくない Irp を、ドライバースタック上の次の下位のドライバーに渡す必要があります。 また、 **FastIoDetachDevice**を実装する必要があります。

**注**   MICROSOFT Windows XP 以降では、次の高速 i/o コールバックルーチンは互換性のために残されています。ファイルシステムフィルタードライバーでは使用できません: **AcquireForCcFlush**

**AcquireFileForNtCreateSection**

**AcquireForModWrite**

**ReleaseForCcFlush**

**Releasefileforntのファイル**

**ReleaseForModWrite**

詳細については、 [**Fsrtlregisterfilesystemfiltercallbacks バック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)のリファレンスエントリを参照してください。

 

 

 




