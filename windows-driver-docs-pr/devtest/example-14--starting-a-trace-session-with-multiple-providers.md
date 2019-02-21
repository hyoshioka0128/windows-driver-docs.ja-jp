---
title: 複数のプロバイダーでトレース セッションを開始する 14 の例
description: 複数のプロバイダーでトレース セッションを開始する 14 の例
ms.assetid: fda63107-608c-4278-abf8-1447c8f8302a
keywords:
- Tracelog WDK、プロバイダー
- プロバイダーの WDK ソフトウェア トレース
- WDK、プロバイダーのトレース
- 複数のプロバイダー WDK ソフトウェア トレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 496a596b75df6c98adcd9808b1ba3a5a50ec9e89
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535571"
---
# <a name="example-14-starting-a-trace-session-with-multiple-providers"></a>14 の使用例:複数のプロバイダーでトレース セッションを開始


## <span id="ddk_starting_a_session_with_multiple_providers_tools"></span><span id="DDK_STARTING_A_SESSION_WITH_MULTIPLE_PROVIDERS_TOOLS"></span>


次のコマンドは、2 つのトレース プロバイダーを使用したトレース セッションを開始します。

```
tracelog -start MyTraces -guid 2guids.guid -f mytraces.etl
```

コマンドの標準的なよう**tracelog-開始**コマンドがで指定されたファイル、 **- guid**パラメーター、2guids.guid、2 つプロバイダーの Guid (行ごとに 1 つ) を次に例が含まれています。

```
1540ff4c-3fd7-4bba-9938-1d1bf31573a7
dab01d4d-2d48-477d-b1c3-daad0ce6f06b
```

このコマンドを送信するときにトレース ログは 2 つのプロバイダーと、1 つのトレース セッションを開始し、両方のプロバイダーを使用します。

プロバイダーは、トレース バッファーとイベントのトレース ログ (.etl) ファイルを共有します。 トレース ログには、各プロバイダーからのトレース メッセージが挿入されました。 任意のフラグと、コマンドで指定されたレベルは、トレース セッションですべてのプロバイダーに適用されます。

両方のトレース プロバイダーを有効になっていることを確認するには、使用、 **tracelog enumguid**コマンドは、次のコマンドに示すようにします。

```
tracelog -enumguid
```

応答では、トレース ログは、ETW に登録されているプロバイダーの一覧を表示し、そのうち 2 つが有効であるを示します。 有効なプロバイダーは、太字で表示されます。

```
c:\Tracelog>tracelog -enumguid
##     Guid                       Enabled  LoggerId Level Flags
------------------------------------------------------------
1046d4b1-fce5-48bc-8def-fd33196af19a     FALSE  0    0    0
4a8aaa94-cfc4-46a7-8e4e-17bc45608f0a     FALSE  0    0    0
196e57d9-49c0-4b3b-ac3a-a8a93ada1938     FALSE  0    0    0
1540ff4c-3fd7-4bba-9938-1d1bf31573a7      TRUE  2    0    0
f12b1984-4c42-11d3-ab7b-00c04f68fcdc     FALSE  0    0    0
1fbecc45-c060-4e7c-8a0e-0dbd6116181b     FALSE  0    0    0
94a984ef-f525-4bf1-be3c-ef374056a592     FALSE  0    0    0
3121cf5d-c5e6-4f37-be86-57083590c333     FALSE  0    0    0
fc4b0d39-e8be-4a83-a32f-c0c7c4f61ee4     FALSE  0    0    0
fc570986-5967-4641-a6f9-05291bce66c5     FALSE  0    0    0
39a7b5e0-be85-47fc-b9f5-593a659abac1     FALSE  0    0    0
dab01d4d-2d48-477d-b1c3-daad0ce6f06b      TRUE  2    0    0k
bca7bd7f-b0bf-4051-99f4-03cfe79664c1     FALSE  0    0    0
d58c126f-b309-11d1-969e-0000f875a5bc     FALSE  0    0    0
d58c126e-b309-11d1-969e-0000f875a5bc     FALSE  0    0    0
58db8e03-0537-45cb-b29b-597f6cbebbfe     FALSE  0    0    0
27246e9d-b4df-4f20-b969-736fa49ff6ff     FALSE  0    0    0
```

セッションで、各トレース プロバイダーのさまざまなフラグとレベルを指定するに個別を使用して、 **tracelog-有効にする**プロバイダーごとのコマンドは、次のコマンドに示すようにします。

```
tracelog -enable MyTraces -guid #1540ff4c-3fd7-4bba-9938-1d1bf31573a7 -flag 2 -level 1
tracelog -enable MyTraces -guid #dab01d4d-2d48-477d-b1c3-daad0ce6f06b -flag 3 -level ffff
```

 

 





