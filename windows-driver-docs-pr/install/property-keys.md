---
title: プロパティのキー
description: プロパティのキー
ms.assetid: 767dbe79-72c6-4445-8d4a-8be53a080825
keywords:
- デバイスのプロパティのキーの WDK デバイス インストールのプロパティ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef08289fb67aa8312a2b29b85fda7615f049ec79
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557012"
---
# <a name="property-keys"></a>プロパティのキー


プログラムでは、すべてのデバイス プロパティ、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)プロパティのキーによって表されます。 プロパティのキーとしてコード化された[ **DEVPROPKEY** ](https://msdn.microsoft.com/library/windows/hardware/ff543544)構造体。 プロパティのキーが定義されている*Devpkey.h*します。

DEVPROPKEY 構造では、次のメンバーがあります。

<a href="" id="fmtid"></a>**fmtid**  
プロパティのカテゴリを識別する DEVPROPGUID に型指定された変数です。

<a href="" id="pid"></a>**pid**  
プロパティの識別子を示す DEVPROPID に型指定された変数です。 内部システム上の理由から、プロパティの識別子が 2 つ以上である必要があります。

カスタムのデバイス プロパティのキーを作成するには、使用、 [ **DEFINE_DEVPROPKEY** ](https://msdn.microsoft.com/library/windows/hardware/ff541072)マクロ。

次に DEFINE_DEVPROPKEY マクロを使用して、DEVPROPKEY 構造を作成する方法の例を示します。 構造の名前に"DEVPROPKEYStructureName"も 0xe0 を通じて 0xde5c254e の値のシーケンス、GUID 値を指定する、値「2」は、プロパティ識別子。

```cpp
DEFINE_DEVPROPKEY(DEVPROPKEYStuctureName, 0xde5c254e, 0xab1c, 0xeffd, 0x80, 0x20, 0x67, 0xd1, 0x46, 0xa8, 0x50, 0xe0, 2)
```

**注**  システム定義のプロパティの主要なカテゴリはシステム専用として予約されています。

 

 

 





