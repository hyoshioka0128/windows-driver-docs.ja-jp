---
title: プロバイダーでの基本的な開始コマンドの例 2
description: プロバイダーでの基本的な開始コマンドの例 2
ms.assetid: 86730943-107e-441a-a860-4df540bc0426
keywords:
- トレース セッションを開始、WDK
- コマンドを開始します。
- -コマンドの開始
- guid パラメーター
- -guid パラメーター
- トレース セッションの起動
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9ad3f3e0687e8e2d494e10d090662d898e290a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553639"
---
# <a name="example-2-basic-start-command-with-provider"></a>例 2:プロバイダーの基本的な Start コマンド

使用する点を除いては、次の開始コマンドは例 1 の場合は、コマンドと同じ、 **- guid**トレース セッションのプロバイダーを有効にするパラメーター。

```
tracelog -start MyTrace -guid #d58c126f-b309-11d1-969e-0000f875a5bc
```

コマンドは、"My Trace"という名前のトレース セッションを開始します。 使用して、 **- guid**コントロールのトレース プロバイダーの GUID を指定するパラメーター。 GUID の先頭に番号記号 (**\#**) を GUID と GUID ファイル名が無効であるかを示します。

応答では、トレース ログは MyTrace トレースのログ セッションを開始し、GUID で指定されたプロバイダーを有効にします。 C: でのログ ファイルの作成を含め、セッションの他のプロパティの既定値を使用して\\LogFile.etl します。

(この例では、"MyTrace") では、トレース セッションの名前を指定しない場合、トレース ログは、既定値は、NT Kernel Logger のトレース セッションを開始します。

フラグまたはレベルを指定しない場合は、有効になっている場合でも、プロバイダーによってはされません、トレース メッセージを生成可能性があります。
