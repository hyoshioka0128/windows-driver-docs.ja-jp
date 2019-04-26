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
ms.openlocfilehash: 85ee67d1928696ea0e49789e21259748af9ff07b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341524"
---
# <a name="filter-device-object-attached-to-a-volume"></a>ボリュームにアタッチされるフィルター デバイス オブジェクト


## <span id="ddk_a_filter_device_object_attached_to_a_volume_if"></span><span id="DDK_A_FILTER_DEVICE_OBJECT_ATTACHED_TO_A_VOLUME_IF"></span>


ボリュームをフィルターするには、フィルター ドライバーは、フィルター デバイス オブジェクトを作成し、ボリュームのボリュームのデバイス オブジェクトの上にアタッチします。

### <a name="span-idtypesofiorequeststhataresenttoavolumespanspan-idtypesofiorequeststhataresenttoavolumespantypes-of-io-requests-that-are-sent-to-a-volume"></a><span id="types_of_i_o_requests_that_are_sent_to_a_volume"></span><span id="TYPES_OF_I_O_REQUESTS_THAT_ARE_SENT_TO_A_VOLUME"></span>ボリュームに送信される I/O 要求の種類

ボリューム上に関連付けられているフィルター デバイス オブジェクトは、次の種類の I/O 要求を受信する概してできます。

[**IRP\_MJ\_クリーンアップ**](https://msdn.microsoft.com/library/windows/hardware/ff548608)

[**IRP\_MJ\_CLOSE**](https://msdn.microsoft.com/library/windows/hardware/ff548621)

[**IRP\_MJ\_CREATE**](https://msdn.microsoft.com/library/windows/hardware/ff548630)

[**IRP\_MJ\_DEVICE\_CONTROL**](https://msdn.microsoft.com/library/windows/hardware/ff548649)

[**IRP\_MJ\_ディレクトリ\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff548658)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff548670)

[**IRP\_MJ\_フラッシュ\_バッファー**](https://msdn.microsoft.com/library/windows/hardware/ff549235)

[**IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff549241)

[**IRP\_MJ\_ロック\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff549251)

[**IRP\_MJ\_PNP**](https://msdn.microsoft.com/library/windows/hardware/ff549268)

[**IRP\_MJ\_クエリ\_EA**](https://msdn.microsoft.com/library/windows/hardware/ff549279)

[**IRP\_MJ\_クエリ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff549283)

[**IRP\_MJ\_クエリ\_クォータ**](https://msdn.microsoft.com/library/windows/hardware/ff549293)

[**IRP\_MJ\_QUERY\_SECURITY**](https://msdn.microsoft.com/library/windows/hardware/ff549298)

[**IRP\_MJ\_クエリ\_ボリューム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff549318)

[**IRP\_MJ\_READ**](https://msdn.microsoft.com/library/windows/hardware/ff549327)

[**IRP\_MJ\_SET\_EA**](https://msdn.microsoft.com/library/windows/hardware/ff549346)

[**IRP\_MJ\_SET\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff549366)

[**IRP\_MJ\_SET\_QUOTA**](https://msdn.microsoft.com/library/windows/hardware/ff549401)

[**IRP\_MJ\_SET\_SECURITY**](https://msdn.microsoft.com/library/windows/hardware/ff549407)

[**IRP\_MJ\_設定\_ボリューム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff549415)

[**IRP\_MJ\_シャット ダウン**](https://msdn.microsoft.com/library/windows/hardware/ff549423)

[**IRP\_MJ\_WRITE**](https://msdn.microsoft.com/library/windows/hardware/ff549427)

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

詳細については、参照のエントリを参照してください。 [ **FsRtlRegisterFileSystemFilterCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff547172)します。

 

 

 




