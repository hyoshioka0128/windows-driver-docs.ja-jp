---
title: デバイス オブジェクトのフラグの確認
description: デバイス オブジェクトのフラグの確認
ms.assetid: f7bff7b8-bd30-4489-ab3f-ca5ad4d5c1ba
keywords:
- リムーバブルメディアの WDK カーネル、フラグチェック
- WDK リムーバブルメディアにフラグをする
- デバイスオブジェクトフラグを確認しています
- デバイスオブジェクトフラグを検証しています
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98602821338a34e34631b36df88d9b2dc80f3af8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837103"
---
# <a name="checking-flags-in-the-device-object"></a>デバイス オブジェクトのフラグの確認





リムーバブルメディアに対する i/o 操作を要求している各 IRP に対して、リムーバブルメディアデバイスドライバーは、 **DeviceObject-&gt;フラグ**で\_ボリュームが既に設定されているかどうかを確認\_かどうかを判断する必要があります。 この値が設定されている場合、ドライバーは次の操作を行う必要があります。

-   [**Irp\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)、 [**irp\_MJ\_WRITE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)、および[**irp\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求については、「」で\_ボリュームが設定されていることを確認するために、SL\_上書きするかどうかを確認します。ドライバーの[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)の構造体の**フラグ**メンバー。 指定されている場合は、要求された操作を続行します。

    基になるメディアの論理構造に関する情報を返すデバイス制御要求では、\_上書きされます。これは、IFS がをマウントまたは再度マウントするときに、i/o スタックの場所の**フラグ**メンバーで\_ボリュームセットを検証\_ます。リムーバブルメディアボリューム。

-   それ以外の場合、ドライバーは、対応するドライブ、デバイス、またはパーティションに対して i/o 要求を実行することを拒否する必要があります\_ボリュームが**DeviceObject&gt;フラグ**で設定されていることを確認\_ます。 リムーバブルメディアドライバーは、前のサブセクションで説明されているように、対応するデバイスに送信される Irp を失敗させる必要があります。 FSD がクリアされるまで、各 IRP に対して手順3と4の両方を繰り返し、リムーバブルメディアドライバーの DeviceObject の\_ボリュームを確認\_ます。 **フラグを&gt;** します。

\_ボリュームが設定されていることを確認\_と SL\_\_上書きするときにリムーバブルメディアデバイスドライバーで Irp が失敗しない場合は、上記の転送要求に対して\_ボリュームが設定されていないことを確認します。ファイルシステムは、キャッシュされたファイルデータは、開いているファイルを保持しているメディアを再マウントするように求められることもありません。

 

 




