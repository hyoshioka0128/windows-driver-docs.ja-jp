---
title: C28168
description: ディスパッチ関数がない警告 C28168、 _Dispatch_type_テーブル エントリのディスパッチに一致する注釈。
ms.assetid: 5e5acc54-acb3-4366-a625-eb79865e932e
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28168
ms.openlocfilehash: b0193771152d701e04b3e39a3bd0586079099a5b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550667"
---
# <a name="c28168"></a>C28168


C28168 を警告します。ディスパッチ関数はありません、 **\_ディスパッチ\_型\_** テーブル エントリのディスパッチに一致する注釈

この警告をサポートしています[Static Driver Verifier](static-driver-verifier.md)ディスパッチ テーブルに割り当てられている各関数が 1 つまたは複数の注釈が付けられたことを確認して**\_ディスパッチ\_型\_** その関数によって実行されたディスパッチ操作の種類を示すの注釈。 コード分析ツールは、関数に対する注釈には、ディスパッチ テーブル エントリのスロットが一致しない場合に、このエラーを報告します。

追加するか、この問題を修正することができます、 **\_ディスパッチ\_型\_** 関数または使用されるディスパッチ テーブル エントリを修正する注釈。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次のコード例では、この警告を生成します。

```
DRIVER_DISPATCH SampleCreate;
...
pDo->MajorFunction[IRP_MJ_CREATE] = SampleCreate;
...
```

次のコード例は、この警告を回避できます。

```
_Dispatch_type_(IRP_MJ_CREATE) DRIVER_DISPATCH SampleCreate;
...
pDo->MajorFunction[IRP_MJ_CREATE] = SampleCreate;
...
```

## <a name="span-idcommentsspanspan-idcommentsspanspan-idcommentsspancomments"></a><span id="Comments"></span><span id="comments"></span><span id="COMMENTS"></span>コメント


状況によっては、この警告を抑制する必要もあります。 いくつかのドライバーでは、たとえば、フィルター ドライバー、他のユーザーを直接登録した後、ループ内でディスパッチ ルーチンを登録する場合があります。

```ManagedCPlusPlus
DriverObject->MajorFunction[IRP_MJ_CREATE]         = DispatchCreate;
DriverObject->MajorFunction[IRP_MJ_READ]           = DispatchRead;
for (Index = 0; Index <= IRP_MJ_MAXIMUM_FUNCTION; Index++)
    {
            DriverObject->MajorFunction[Index] = DispatchPassIrp;
    }
```

この例で、 **DispatchPassIrp**関数は、次の注釈では宣言されて正しく。

```ManagedCPlusPlus
__drv_dispatchType(IRP_MJ_CREATE_NAMED_PIPE)
__drv_dispatchType(IRP_MJ_QUERY_INFORMATION)
// .... 
//  (additional dispatch type annotations) 
// ....
__drv_dispatchType(IRP_MJ_CREATE_NAMED_PIPE)
    DRIVER_DISPATCH DispatchPassIrp;
```

このような状況では、コード分析ツールは、このエラーを報告します。

```
The function 'DispatchPassIrp' does not have a _Dispatch_type_ annotation matching dispatch table position 'IRP_MJ_CREATE' (0x00):  This can be  corrected either by adding a _Dispatch_type_ annotation to the function declaration or correcting the dispatch table entry being used.
```

このディスパッチ テーブル内のループの使用は、いくつかのフィルター ドライバーで一般的です。 このような状況で、エラー メッセージは無視できます、これは、静的分析の制限とします。 コード分析ツールは、関数に対する注釈には、ディスパッチ テーブル エントリのスロットが一致しない場合に、このエラーを報告します。 コード分析ツールが、無効な代入を報告この例では、(を後で元に)。 ただしがない無効な状態にしないことを元に戻すを把握する静的ツールの以降です。 これによりと後でそれらの修正、割り当てを行うことがわかっている場合は、警告を抑制できます。

 

 





