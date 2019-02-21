---
title: C28169
description: 警告 C28169 ディスパッチ関数が含まれない_Dispatch_type_注釈。
ms.assetid: ce33993f-f967-43b0-89fb-d8553517aae3
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28169
ms.openlocfilehash: 18719142bb32fd32fada4cdd8db479d3c112ab1f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558167"
---
# <a name="c28169"></a>C28169


C28169 を警告します。ディスパッチ関数が含まれない**\_ディスパッチ\_型\_** 注釈

コード分析ツールは、この警告を報告への代入の右側にある、 **MajorFunction**テーブルがあるない (有効) **\_ディスパッチ\_型\_** 注釈。 右側にあるが、キャストを削除する場合、警告は発生場合があります、 **\_ディスパッチ\_型\_** 注釈。 右側にあるドライバーの種類の関数である必要があります\_と適切なディスパッチ タイプ**\_ディスパッチ\_型\_** 注釈。

詳細については、次を参照してください。[を使用して関数の役割の型の宣言](using-function-role-type-declarations.md)します。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次の関数宣言が関数のディスパッチの日常的な割り当てで使用する場合、この警告を引き起こします、 **MajorFunction**します。

```
NTSTATUS
DispatchSystemControl (
    PDEVICE_OBJECT  DeviceObject,
    PIRP            Irp
    );
```

同様で使用される、次の関数宣言には、この警告考えつくされません。

```
// Function: DispatchSystemControl
// This is an example of a fully annotated declaration.  
// IRP_MJ_SYSTEM_CONTROL is the type of IRP handled by this function.  
// Multiple _Dispatch_type_ lines are acceptable if the function handles more than 1 IRP type.
//
_Dispatch_type_(IRP_MJ_SYSTEM_CONTROL) 
DRIVER_DISPATCH DispatchSystemControl;
```

 

 





