---
title: 更新されたコアのドライバー パッケージを取得します。
description: 更新されたコアのドライバー パッケージを取得します。
ms.assetid: 7fac00e4-1d3e-4bb7-95cd-298176de374d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27a842159c15ef3cf86e39a8048854e0fd5137b7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551194"
---
# <a name="getting-the-updated-core-driver-package"></a>更新されたコアのドライバー パッケージを取得します。


したら[取得](constructing-a-package-aware-driver-with-updated-core-drivers.md)中核となる更新されたドライバー パッケージを含む Microsoft のスタンドアロン更新プログラム (MSU) ファイル、[次へ] の手順では MSU ファイルの内容を展開します。

Core のドライバー パッケージの内容を PnP インストーラーにアクセスできるようにするには、コマンド プロンプト ウィンドウを開くし、[展開] コマンドを使用して、MSU ファイルを展開します。 また、「Windows6.0-」、MSU ファイルに含まれるで始まる名前を持つ適切なキャビネット (.cab) ファイルを展開します。

次の例は、使用する方法を示します、**展開**コマンドで、MSU ファイルが含まれているディレクトリで実行する必要があります。

```cpp
expand Windows6.0-KB123456-x86.MSU [dest directory] -F:*
expand Windows6.0-KB123456-x86.CAB [dest directory] -F:*
```

これら 2 つのコマンドでは、次のディレクトリにはさまざまなマニフェスト ファイルとサブディレクトリが含まれます。 これらのサブディレクトリの 1 つは、Ntprint.inf と圧縮されていないドライバーのコンポーネントが含まれます。 このディレクトリは、追加された"ntprint.inf"、GUID、およびその他の追跡情報が修正プログラム (たとえば、x86) のプロセッサ アーキテクチャで始まる名前を持っています。 詳細については、の定義を参照してください、**展開**microsoft コマンド[TechNet](https://go.microsoft.com/fwlink/p/?linkid=122164) Web サイト。

 

 




