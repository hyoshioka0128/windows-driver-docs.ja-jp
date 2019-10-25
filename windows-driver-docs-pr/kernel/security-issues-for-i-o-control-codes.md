---
title: I/O 制御コードに関するセキュリティの問題
description: I/O 制御コードに関するセキュリティの問題
ms.assetid: cab8aed2-7185-4622-9a8f-bc8eab3c8c59
keywords:
- I/o 制御コード WDK カーネル、セキュリティ
- コントロールコード WDK Ioctl、セキュリティ
- Ioctl WDK カーネル、セキュリティ
- セキュリティ WDK Ioctl
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e98a13051335768bececd394ee6add20bcd925ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836379"
---
# <a name="security-issues-for-io-control-codes"></a>I/O 制御コードに関するセキュリティの問題





I/o 制御コードを含む Irp のセキュリティで保護された処理は、IOCTL コードを適切に定義し、ドライバーが IRP で受信するパラメーターを慎重に調べることに依存します。

新しい IOCTL コードを定義する場合は、次の規則を使用します。

-   常に、0x800 以上の*Functioncode*値を指定してください。

-   常に*Requiredaccess*値を指定します。 I/o マネージャーは、呼び出し元に十分なアクセス権がない場合、Ioctl を送信しません。

-   呼び出し元がカーネルメモリの不特定の領域の読み取りまたは書き込みを実行できるようにする IOCTL コードを定義しないでください。

ドライバー内で IOCTL コードを処理するときは、次の規則を使用します。

-   ドライバーのディスパッチルーチンは、受け取った IOCTL コードをテストするたびに、常に32ビット値全体をテストする必要があります。

-   ドライバーは、 [**IoValidateDeviceIoControlAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iovalidatedeviceiocontrolaccess)を使用して、i/o 制御コードの定義で、 *requiredaccess*値で指定されたより厳密なアクセスチェックを動的に実行できます。

-   Irp&gt;AssociatedIrp が指すバッファーよりも多くのデータを読み書きすることはできません **。 SystemBuffer**にはを含めることができます。 したがって、 [**IO\_STACK\_LOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)構造体の**DeviceIoControl**または**DeviceIoControl の長さ**を常に確認して、バッファーの制限を決定します。

-   IOCTL 要求を送信したアプリケーションを対象としたデータを含む、ドライバーで割り当てられたバッファーは常にゼロになります。 このようにすると、機密データが誤ってアプリケーションにコピーされることはありません。

-   \_DIRECT およびメソッドで\_メソッドを使用して直接転送\_\_するには、上記のルールに従います。 さらに、 [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)から**NULL**の戻り値があるかどうかを確認します。これは、マッピングが失敗したか、長さが0のバッファーが指定されたことを示します。

-   メソッド\_転送のどちらでもない場合は、[バッファーも直接 I/o も使用せず](using-neither-buffered-nor-direct-i-o.md)に、に用意されている規則に従います。

 

 




