---
title: スタティック ライブラリで WPP を使用する方法
description: スタティック ライブラリで WPP を使用する方法
ms.assetid: 02e13837-f8c7-4824-a4db-5e8b49fdcb59
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b24dbd13c108e0e9e16c139354eab9dd5be8985e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390533"
---
# <a name="how-do-i-use-wpp-in-static-libraries"></a>スタティック ライブラリで WPP を使用する方法


WPP トレースを使用できるスタティック ライブラリ (.lib) とバイナリ (.exe、.dll または .sys) のトレースを個別の制御を提供するように静的ライブラリ内で使用します。

バイナリとライブラリの両方がある独自のコントロールの GUID。 これにより、スタティック ライブラリ、バイナリ、またはその両方で有効にするトレースします。

.Lib ファイルは、次のコード例に示すように、いくつかの時点では、WPP を使用してアクセスできます。 GUID では、コントロールの実際の値を定義する重要なスタティック ライブラリには、WPP は呼び出さないため、注意してください\_INIT\_トレース マクロは、ETW を使用した実際の登録をしています。

```
#define WPP_CONTROL_GUIDS \
WPP_DEFINE_CONTROL_GUID(mylib,(0,0,0,0,0), \
WPP_DEFINE_BIT(Error) \
WPP_DEFINE_BIT(Unusual) \
WPP_DEFINE_BIT(Noise) \
)
```

ライブラリを使用して、.dll、.exe、および .sys ファイルは、WPP を呼び出す必要があります\_INIT\_トレースで、WPP プロバイダーに登録されます。 呼び出すマクロ WPP バイナリ\_INIT\_トレースは、WPP コントロール、WPP で取得した Guid のコピーを用意する必要があります\_コントロール\_GUID マクロ。 スタティック ライブラリで定義されているフラグは、バイナリでも使用する予定の場合にのみフラグの値のコピーが必要です。

次のコード サンプルでスタティック ライブラリのコントロールの GUID が最初に宣言し、ライブラリで定義されているフラグに一致するコントロールの GUID のフラグ。

```
#define WPP_CONTROL_GUIDS \
WPP_DEFINE_CONTROL_GUID(SharedStaticLibs,(81b20feb,73a8,4b62,95bc,354477c97a6f), \
WPP_DEFINE_BIT(Error) \
WPP_DEFINE_BIT(Unusual) \
WPP_DEFINE_BIT(Noise) \
) \
WPP_DEFINE_CONTROL_GUID(AppSpecificFlags,(81b20fec,73a8,4b62,95bc,354477c97a6f), \
WPP_DEFINE_BIT(EntryExit) \
WPP_DEFINE_BIT(Initialization) \
WPP_DEFINE_BIT(MemoryAllocations) \
) 
```

必要なトレースのコンポーネントと静的ライブラリの両方で両方のそれぞれに独自のフラグ、.lib、および、.exe ファイルの個別のコントロールの GUID または GUID の 1 つのコントロールのいずれかを指定することで制御のレベルを選択できます。 サンプルでは、.exe ファイルは .lib ファイルとして同じフラグを使用します。

 

 





