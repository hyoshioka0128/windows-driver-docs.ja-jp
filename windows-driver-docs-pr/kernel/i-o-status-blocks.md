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
ms.openlocfilehash: 2e5cc1286d49e4b6b48343b0248f83dc4bd46280
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572668"
---
# <a name="io-status-blocks"></a>I/O ステータス ブロック





構成される、I/O 状態ブロック、 [ **IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)構造体をそれぞれの一部である[ **IRP** ](https://msdn.microsoft.com/library/windows/hardware/ff550694). 状態の I/O のブロックには、2 つの目的があります。

-   高度なドライバーの提供[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) IRP が完了したときに、サービスが動作するかどうかを判断する方法、ルーチン。

-   これは、理由、サービス動作または動作しなかった詳細情報を提供します。

、、の IRP の完了時に、**状態**フィールドは、ドライバーが IRP の処理が実際には、要求を満たすか、IRP がエラー状態が失敗したかを示します。 **情報**フィールドは、呼び出し元に実際に発生した内容についての詳細情報を提供します。 たとえば、読み取りまたは書き込み操作の後に実際に転送されたバイト数が含まれています。

詳細については、[IRP の状態の I/O ブロックを設定](processing-irps-in-a-lowest-level-driver.md#ddk-setting-the-i-o-status-block-in-an-irp-kg)を参照してください。

 

 




