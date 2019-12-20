---
title: 更新されたコア ドライバー パッケージを取得する
description: 更新されたコア ドライバー パッケージを取得する
ms.assetid: 7fac00e4-1d3e-4bb7-95cd-298176de374d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f92bf4d0523217ed0d4fe47fbeb45fcb28e88a28
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210906"
---
# <a name="getting-the-updated-core-driver-package"></a>更新されたコア ドライバー パッケージを取得する

更新されたコアドライバーパッケージを含む Microsoft スタンドアロン更新プログラム (MSU) ファイルを[入手](constructing-a-package-aware-driver-with-updated-core-drivers.md)したら、次の手順として、MSU ファイルの内容を展開します。

コアドライバーパッケージの内容を PnP インストーラーからアクセスできるようにするには、コマンドプロンプトウィンドウを開き、expand コマンドを使用して MSU ファイルを展開します。 また、適切なキャビネット (.cab) ファイルを展開します。このファイルには、MSU ファイルに含まれる "Windows 6.0-" で始まる名前が付いています。

次の例では、[**展開**](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-xp/bb490903(v=technet.10))コマンドを使用する方法を示します。このコマンドは、MSU ファイルが格納されているディレクトリで実行する必要があります。

```cpp
expand Windows6.0-KB123456-x86.MSU [dest directory] -F:*
expand Windows6.0-KB123456-x86.CAB [dest directory] -F:*
```

この2つのコマンドの後に、ディレクトリには多数のマニフェストファイルとサブディレクトリが含まれます。 これらのサブディレクトリの1つには、Ntprint.inf および圧縮されていないドライバーコンポーネントが含まれます。 このディレクトリの名前は、修正プログラムのプロセッサアーキテクチャ (x86 など) で始まり、"ntprint.inf"、GUID、および追加の追跡情報が追加されます。
