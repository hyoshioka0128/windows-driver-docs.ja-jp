---
title: PFA メモリの一覧を管理する方法
description: PFA メモリの一覧を管理する方法
ms.assetid: 28463f91-275b-4ad4-af64-59bed7fd3806
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9b8e74e2307f7e8da4d02db62368c164336a55a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559720"
---
# <a name="how-to-manage-the-pfa-memory-list"></a>PFA メモリの一覧を管理する方法


表示および BCDEdit のコマンド ライン ツールを使用して、BCD システム ストアに保存されているメモリ ページの一覧を削除できます。 BCDEdit ツールを使用するには、コンピューターの Administrators グループのメンバーであるし、BCDEdit を管理者特権でコマンド プロンプトから実行する必要があります。 管理者特権でコマンド プロンプト ウィンドウを開くには、次の手順に従います。

1.  をクリックして**開始**、 をポイント**すべてのプログラム**、順にクリックします**アクセサリ**します。

2.  **[コマンド プロンプト]** を右クリックし、**[管理者として実行]** をクリックします。

3.  ユーザー アカウント制御 ダイアログ ボックスが表示されたらクリックして**はい** ダイアログ ボックス。

### <a name="viewing-the-current-list-of-pfns"></a>PFNs の現在の一覧を表示します。

システムの BCD ストアで PFNs の現在の一覧を表示するには、次のコマンドを実行します。

``` syntax
C:\Windows\system32>bcdedit /enum {badmemory}
```

失敗する ECC メモリ ページが予測されることはありません、次の例のように、BCDEdit ツールからの出力が表示されます。

``` syntax
C:\Windows\system32>bcdedit /enum {badmemory}

RAM Defects
-----------
identifier              {badmemory}
```

ECC メモリ ページが失敗すると、予測される場合、 **{badmemory}** オブジェクトが含まれています、 **badmemorylist**値。 この値には、次の例に示すように PFA を予測するページが失敗すると、メモリの PFNs の一覧が含まれています。

``` syntax
C:\Windows\system32>bcdedit /enum {badmemory}

RAM Defects
-----------
identifier              {badmemory}
badmemorylist           0xffe38
                        0x100f
```

### <a name="clearing-the-current-list-of-pfns"></a>PFNs の現在の一覧の消去

PFNs BCD システム ストアの一覧をクリアするには、次のコマンドを実行します。

``` syntax
C:\Windows\system32>bcdedit /deletevalue {badmemory} badmemorylist
```

**注**  不適切な変更 BCD システム ストアは、以降から Windows を防ぐことができます。 そのため、する必要がありますコマンドと結果を確認、慎重に Windows を再起動する前にします。

 

 

 




