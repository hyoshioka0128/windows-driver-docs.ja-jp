---
title: I/O 制御コードに関するセキュリティの問題
description: I/O 制御コードに関するセキュリティの問題
ms.assetid: cab8aed2-7185-4622-9a8f-bc8eab3c8c59
keywords:
- I/O 制御コード WDK カーネルのセキュリティ
- 制御コード WDK Ioctl、セキュリティ
- Ioctl WDK カーネルでは、セキュリティ
- WDK の Ioctl セキュリティ
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 254f1da8b2e4ab3c9cf66c0996de6164d87ec902
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373375"
---
# <a name="security-issues-for-io-control-codes"></a>I/O 制御コードに関するセキュリティの問題





I/O 制御コードが含まれている Irp の処理をセキュリティで保護されたは、IOCTL コードを適切に定義して、ドライバーが IRP を受信したパラメーターを注意深く確認することによって異なります。

新しい IOCTL コードを定義するときに、次の規則を使用します。

-   常に指定する*FunctionCode* 0x800 以上である値。

-   常に指定する*RequiredAccess*値。 I/O マネージャーでは、呼び出し元に十分なアクセス権がある場合、Ioctl は送信しません。

-   読み取りまたは書き込みのカーネル メモリの不特定の領域を呼び出し元を許可 IOCTL コードを定義してください。

ドライバー内での IOCTL コードを処理する際は、次の規則を使用します。

-   ドライバーのディスパッチ ルーチンは、受信した IOCTL コードをテストするときに、常に 32 ビット値全体をテストする必要があります。

-   ドライバーを使用できる[ **IoValidateDeviceIoControlAccess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iovalidatedeviceiocontrolaccess)より厳密なアクセスを動的に実行するで指定されたチェック、 *RequiredAccess*値で、I/O 制御コードの定義。

-   読み取りまたはによってポイントされているバッファーよりも多くのデータを記述しないでください**Irp -&gt;AssociatedIrp.SystemBuffer**含めることができます。 そのため、常に確認**Parameters.DeviceIoControl.InputBufferLength**または**Parameters.DeviceIoControl.OutputBufferLength**で、 [ **IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)バッファーの制限を決定する構造体。

-   IOCTL 要求を開始したアプリケーションは、データが格納されるドライバーに割り当てられたバッファーは常に 0 します。 そうすることはない誤ってデータをコピーする機密性の高いアプリケーションにします。

-   メソッドの\_IN\_ダイレクトとメソッド\_アウト\_転送を直接、上記のルールに従ってください。 さらに、確認、 **NULL**から値を返す[ **MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)マッピングが失敗したこと、または長さ 0 のバッファーが指定されていることを示します。

-   メソッドの\_どちらの転送に用意されている規則に従う[を使用していないバッファー Nor ダイレクト I/O](using-neither-buffered-nor-direct-i-o.md)します。

 

 




