---
title: I/o 状態ブロック
description: I/o 状態ブロック
ms.assetid: 59147bd1-6cd7-4fbe-b7bc-52e09ab88576
keywords:
- Irp WDK カーネル、i/o 状態ブロック
- I/o ステータスが WDK カーネルをブロックする
- 状態は WDK カーネルをブロックします
- IO_STATUS_BLOCK 構造体
- ステータス情報 WDK Irp
- Irp WDK カーネル、状態情報
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab5d8c8a203a88db2f63a8c64cd1ee9b0002f032
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838641"
---
# <a name="io-status-blocks"></a>I/o 状態ブロック





I/o 状態ブロックは、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造で構成され、各[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)の一部です。 I/o 状態ブロックは、次の2つの目的で機能します。

-   これにより、IRP の完了時にサービスが動作しているかどうかを判断するための、より高度なドライバーの[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンが提供されます。

-   これにより、サービスが動作しているのか、機能しなかったのかについての詳細情報が提供されます。

IRP が完了すると、**状態**フィールドは、irp を処理したドライバーが実際に要求を満たしているかどうか、またはエラー状態の irp に失敗したかどうかを示します。 **情報**フィールドは、実際に発生した内容に関する詳細情報を呼び出し元に提供します。 たとえば、読み取り操作または書き込み操作の後に実際に転送されたバイト数が含まれます。

詳細については、「 [IRP での I/o ステータスブロックの設定](processing-irps-in-a-lowest-level-driver.md#ddk-setting-the-i-o-status-block-in-an-irp-kg)」を参照してください。

 

 




