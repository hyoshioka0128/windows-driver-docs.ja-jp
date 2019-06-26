---
title: フレームワーク オブジェクトのカスタム型
description: フレームワーク オブジェクトのカスタム型
ms.assetid: E00393ED-7285-4354-9E1B-D9ABDB7DC9F2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c32d06367a86a3d27561afb28a368803abab664
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382867"
---
# <a name="framework-object-custom-types"></a>フレームワーク オブジェクトのカスタム型


KMDF バージョン 1.11 以降、フレームワークには、カスタムの型名がサポートしています。 カスタムの型名は、文字列は、ドライバーが WDFOBJECT インスタンスに関連付けることができます。 ドライバーは、独自のカスタムの型名を定義します。 ドライバーでは、ドライバーが、オブジェクトの作成メソッドを呼び出した後、オブジェクトのカスタムの型名を指定します。

カスタムの型名を操作するのにには、これらのマクロを使用します。

-   カスタム型の名前を定義するには、呼び出す[ **WDF\_DECLARE\_カスタム\_型**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdf-declare-custom-type)ヘッダー ファイルなどのグローバル データを宣言するドライバーの領域から。
-   呼び出す[ **WdfObjectAddCustomType** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectaddcustomtype)または[ **WdfObjectAddCustomTypeWithData** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectaddcustomtypewithdata) framework オブジェクトにカスタム型を関連付ける。
-   呼び出す[ **WdfObjectIsCustomType** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectiscustomtype)に指定したオブジェクトが、指定したカスタム型かどうかを判断します。
-   呼び出した後[ **WdfObjectAddCustomTypeWithData**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectaddcustomtypewithdata)、ドライバーは後で呼び出すことができます[ **WdfObjectGetCustomTypeData** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectgetcustomtypedata)を取得しますデータ。

ドライバーは、複数のカスタム型を 1 つのフレームワーク オブジェクトに関連付けることができます。 ドライバーでは、1 つのカスタム型を複数のフレームワーク オブジェクトを関連付けることもします。

KMDF デバッガー拡張機能からの出力ではカスタム型の名前は WDF オブジェクトの他の情報と共に表示されます。

```cpp
WDF_Object_Name, [custom_Type1_Name, custom_Type2_Name]
```

 

 





