---
title: I/O ステータス ブロック
description: I/O ステータス ブロック
ms.assetid: 59147bd1-6cd7-4fbe-b7bc-52e09ab88576
keywords:
- Irp WDK カーネルでは、I/O の状態のブロック
- I/O 状態ブロック WDK カーネル
- 状態ブロックの WDK カーネル
- IO_STATUS_BLOCK 構造体
- WDK Irp のステータス情報
- Irp WDK カーネルでは、状態情報
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d64f0b90d6105b0d8f8c6645d7e84492d2599e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371858"
---
# <a name="io-status-blocks"></a>I/O ステータス ブロック





構成される、I/O 状態ブロック、 [ **IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)構造体をそれぞれの一部である[ **IRP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp). 状態の I/O のブロックには、2 つの目的があります。

-   高度なドライバーの提供[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) IRP が完了したときに、サービスが動作するかどうかを判断する方法、ルーチン。

-   これは、理由、サービス動作または動作しなかった詳細情報を提供します。

、、の IRP の完了時に、**状態**フィールドは、ドライバーが IRP の処理が実際には、要求を満たすか、IRP がエラー状態が失敗したかを示します。 **情報**フィールドは、呼び出し元に実際に発生した内容についての詳細情報を提供します。 たとえば、読み取りまたは書き込み操作の後に実際に転送されたバイト数が含まれています。

詳細については、次を参照してください。 [IRP の状態の I/O ブロックを設定](processing-irps-in-a-lowest-level-driver.md#ddk-setting-the-i-o-status-block-in-an-irp-kg)します。

 

 




