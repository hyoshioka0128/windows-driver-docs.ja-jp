---
title: ファイル システムにアタッチされるフィルター デバイス オブジェクト
description: ファイル システムにアタッチされるフィルター デバイス オブジェクト
ms.assetid: 5fb0ec43-a639-4b2a-8057-3313e9dee457
keywords:
- デバイス オブジェクトの WDK ファイル システム フィルターをかける
- デバイス オブジェクトの I/O 要求の WDK ファイル システム
- デバイス オブジェクトの I/O 要求ドライバー WDK のファイル システムをフィルター処理します。
- ファイル システム フィルター ドライバー WDK、デバイス オブジェクトの I/O 要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ac461c09b91c00ec11118f1cc0907d751e22227
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341520"
---
# <a name="filter-device-object-attached-to-a-file-system"></a>ファイル システムにアタッチされるフィルター デバイス オブジェクト


## <span id="ddk_a_filter_device_object_attached_to_a_file_system_if"></span><span id="DDK_A_FILTER_DEVICE_OBJECT_ATTACHED_TO_A_FILE_SYSTEM_IF"></span>


全体のファイル システムをフィルターするには、ファイル システム フィルター ドライバーは、フィルター デバイス オブジェクトを作成し、グローバル ファイル システムのキュー内のファイル システム ドライバーの CDO 上結び付けます。

### <a name="span-idtypesofiorequeststhataresenttoafilesystemspanspan-idtypesofiorequeststhataresenttoafilesystemspantypes-of-io-requests-that-are-sent-to-a-file-system"></a><span id="types_of_i_o_requests_that_are_sent_to_a_file_system"></span><span id="TYPES_OF_I_O_REQUESTS_THAT_ARE_SENT_TO_A_FILE_SYSTEM"></span>ファイル システムに送信される I/O 要求の種類

ファイル システム上に関連付けられているフィルター デバイス オブジェクトは、次の種類の I/O 要求を受信する概してできます。

[**IRP\_MJ\_DEVICE\_CONTROL**](https://msdn.microsoft.com/library/windows/hardware/ff548649)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff548670)

[**IRP\_MJ\_シャット ダウン**](https://msdn.microsoft.com/library/windows/hardware/ff549423)

ファイル システムでは、コントロール、そのデバイス オブジェクトを開く処理をサポートする場合は、同様の I/O 要求の次の種類を確認するフィルターが想定されます。

[**IRP\_MJ\_クリーンアップ**](https://msdn.microsoft.com/library/windows/hardware/ff548608)

[**IRP\_MJ\_CLOSE**](https://msdn.microsoft.com/library/windows/hardware/ff548621)

[**IRP\_MJ\_CREATE**](https://msdn.microsoft.com/library/windows/hardware/ff548630)

ドライバー スタックで、次の下位ドライバーにすべての認識できない、または望ましくない Irp を渡すには、既定ではファイル システムにアタッチされたファイル システム フィルター デバイス オブジェクトが必要です。

 

 




