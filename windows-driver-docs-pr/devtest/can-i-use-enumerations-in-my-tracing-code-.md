---
title: トレース コードで列挙型を使用できます。
description: トレース コードで列挙型を使用できます。
ms.assetid: c42ab1ad-6b8f-458f-ba29-e3553095c853
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 098abf6d7e5374b7e165beb3b82f59bf1ead41b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552269"
---
# <a name="can-i-use-enumerations-in-my-tracing-code"></a>列挙体を使用して、トレース コードでできますか。


列挙体を使用すると、ユーザーをデコードする必要がありますの整数値を表示する代わりに、トレース メッセージに意味のある条件を表示します。

たとえば、コードで次の列挙型を定義します。

```
#define SPECIALDAY  0xF0000000
enum _wday {
  sunday = 0,
  monday = 55,
  tuesday = 3,
  wednesday = 1 | SPECIALDAY  ,
  thursday =  7 | SPECIALDAY,
  friday =  5,
  saturday = 6
};
```

列挙体で、トレース メッセージを使用するには、ソース ファイルに次の構成データを追加します。 このコードは、列挙型のシンボル情報を抽出する WPP を指示し、列挙体を表示するときに定義した名前を使用する値を記録します。

```
// begin_wpp config 
// CUSTOM_TYPE(dayset, ItemEnum(_wday) );
// end_wpp
```

使用することができます、 **dayset**トレース メッセージの書式指定文字列にカスタムの型。 次に、例を示します。

```
 _wday p = wednesday;

 DoTraceMessage(NOISE " %!dayset!", p);
```

最後に、非構成ファイル (.ini ファイル以外のファイル) に構成データを追加するため、追加、 **-スキャン**、実行するようにパラメーター\_WPP マクロは、WPP プリプロセッサを呼び出します。 これには、指定したファイルで構成データを検索する WPP に通知します。 次に、例を示します。

```
RUN_WPP -scan:trace.c
```









