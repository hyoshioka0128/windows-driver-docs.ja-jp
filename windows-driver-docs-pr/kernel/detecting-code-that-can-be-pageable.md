---
title: ページング可能にできるコードの検出
description: ページング可能にできるコードの検出
ms.assetid: 5e8a021d-09c3-4e63-b5a8-7559c384ae3d
keywords:
- ページング可能なドライバー WDK カーネルでは、コードの検出
- ページング可能なコードを検出します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a983aa1423e40664010c813f26ef8a12c82eebdc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574670"
---
# <a name="detecting-code-that-can-be-pageable"></a>ページング可能にできるコードの検出





IRQL で実行されるコードを検出するために&gt;= ディスパッチ\_レベル、使用、 [**ページ\_コード**](https://msdn.microsoft.com/library/windows/hardware/ff558773)マクロ。 IRQL でコードが実行されている場合、デバッグ モードでこのマクロがメッセージを生成&gt;= ディスパッチ\_レベル。 次の例のように、ページングされたコードとして全体のルーチンをマークするルーチンの最初のステートメントとしてマクロを追加します。

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

正しくこのことを確認するには、実行、 [Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)に完成したドライバーに対して、**強制 IRQL 検査**オプションを有効にします。 このオプションにより、システム ページング可能なすべてのコードを自動的にページをディスパッチする IRQL をドライバーにさせるたび\_レベルまたはそれ以降。 Driver Verifier を使用して、この領域でのすべてのドライバーのバグをすばやく検索できます。 それ以外の場合、顧客によってのみ通常これらのバグが見つかり、頻繁に、再現するための非常に困難することができます。

 

 




