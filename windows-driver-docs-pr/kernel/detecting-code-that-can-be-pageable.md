---
title: ページング可能にできるコードの検出
description: ページング可能にできるコードの検出
ms.assetid: 5e8a021d-09c3-4e63-b5a8-7559c384ae3d
keywords:
- ページング可能なドライバー WDK カーネルでは、コードの検出
- ページング可能なコードを検出します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fa3027cef0f812845d03128c969aa7fdfe53c7a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371268"
---
# <a name="detecting-code-that-can-be-pageable"></a>ページング可能にできるコードの検出





IRQL で実行されるコードを検出するために&gt;= ディスパッチ\_レベル、使用、 [**ページ\_コード**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)マクロ。 IRQL でコードが実行されている場合、デバッグ モードでこのマクロがメッセージを生成&gt;= ディスパッチ\_レベル。 次の例のように、ページングされたコードとして全体のルーチンをマークするルーチンの最初のステートメントとしてマクロを追加します。

```cpp
NTSTATUS 
MyDriverXxx( 
    IN OUT PVOID ParseContext OPTIONAL, 
    OUT PHANDLE Handle 
    ) 
{ 
    NTSTATUS Status; 
 
    PAGED_CODE(); 
. 
. 
. 
} 
```

正しくこのことを確認するには、実行、 [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)に完成したドライバーに対して、**強制 IRQL 検査**オプションを有効にします。 このオプションにより、システム ページング可能なすべてのコードを自動的にページをディスパッチする IRQL をドライバーにさせるたび\_レベルまたはそれ以降。 Driver Verifier を使用して、この領域でのすべてのドライバーのバグをすばやく検索できます。 それ以外の場合、顧客によってのみ通常これらのバグが見つかり、頻繁に、再現するための非常に困難することができます。

 

 




