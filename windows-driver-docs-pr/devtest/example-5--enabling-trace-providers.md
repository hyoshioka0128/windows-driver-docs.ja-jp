---
title: 例 5 を有効にするトレース プロバイダー
description: 例 5 を有効にするトレース プロバイダー
ms.assetid: 405aea85-0248-4fd3-82eb-1beb76cc8a1b
keywords:
- Tracelog WDK、プロバイダー
- プロバイダーの WDK ソフトウェア トレース
- WDK、プロバイダーのトレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 275e45d68b20694325270788883132626a941f42
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344646"
---
# <a name="example-5-enabling-trace-providers"></a>例 5:トレース プロバイダーの有効化

次のコマンドは、"MyTrace"という名前の実行中のトレース セッションのトレース プロバイダーを有効します。

```
tracelog -enable MyTrace -guid MyProvider.guid
```

応答、Tracelog MyProvider.guid ファイルの Guid で表される、プロバイダーを使用できます。 コマンドでは、トレース セッションの他のプロパティは変更されません。

トレース セッションを開始してから、プロバイダーを有効にまたはトレース セッションの開始中に、プロバイダーを有効にすることができます。 たとえば、次のコマンドは、トレース セッションを開始し、し、プロバイダーを有効にします。

```
tracelog -start MyTrace
tracelog -enable MyTrace -guid MyProvider.guid
```

これに対し、次のコマンドは、セッションを開始し、により、1 つのコマンドでプロバイダー。

```
tracelog -start MyTrace -guid MyProvider.guid
```

以外の相違点のタイミング、これらのコマンドの効果は同じです。

通常、 **tracelog-有効にする**フラグと、プロバイダーに関連付けられているレベルを変更するコマンドを使用します。 フラグとレベルが、トレース セッションのプロパティではなく、プロバイダーのプロパティを使用する、 **tracelog-有効にする**コマンドが、 **tracelog-更新**コマンドは、それらを変更します。

次のコマンドは、MyProvider.guid ファイルでプロバイダーのフラグとレベルを変更します。 使用する必要があります、 **- guid**パラメーターをそのプロバイダーが、唯一のプロバイダーのトレース セッションを有効になっている場合でも、トレース プロバイダーを指定します。

```
tracelog -enable MyTrace -guid MyProvider.guid -flag 2 -level 2
```

使用することも、 **tracelog-を有効にする**コマンドを使用して無効にしているプロバイダーを再度有効にして、トレース セッションに複数のプロバイダーを追加する、 **tracelog-を無効にする**コマンド。
