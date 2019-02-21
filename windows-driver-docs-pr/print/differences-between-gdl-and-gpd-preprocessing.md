---
title: GDL と GPD 前処理の違い
description: GDL と GPD 前処理の違い
ms.assetid: 0ca79e85-1697-4f8d-b534-fe24748aaf5b
keywords:
- GPD ファイル エントリ WDK Unidrv、プリプロセッサ ディレクティブ
- WDK Unidrv、vs GPD ファイルのエントリ。GDL ファイルのエントリ
- GDL WDK、vs GPD
- WDK GDL、vs のプリプロセッサ ディレクティブです。GDL 前処理
- WDK GDL、ソース ファイルのプリプロセッサ ディレクティブのディレクティブ
- ソース ファイル WDK GDL、プリプロセッサ ディレクティブ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 656b294f610e4e65fc03c1cf29da6fafbd8df319
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559142"
---
# <a name="differences-between-gdl-and-gpd-preprocessing"></a>GDL と GPD 前処理の違い


GPD 実装では存在しなかった GDL には、次の 4 つの新しいプリプロセッサ ディレクティブがあります。**\#プリコンパイル済み**、  **\#UndefinePrefix**、  **\#EnablePPDirective**、および **\#DisablePPDirective**します。

さらに、 **\#定義を解除**ディレクティブ受け入れるようになりましたもない引数。 引数がない場合は、最近に定義されたシンボルが定義されていないことを意味する以前に定義されたシンボルを復元します。

GDL ファイルは GPD パーサーで解析するためのものも場合これらの新しいディレクティブを使用しないことをお勧めします。 場合は、GDL に新しいプリプロセッサ ディレクティブをファイルを組み込む tp は GPD パーサーを対象にしても、(旧バージョンと互換性) の代替パスにあるこれらの新しいディレクティブの実行を回避するために古いプリプロセッサを利用できる提供にある必要があります。 各パスは内で囲む必要があります、  **\#Ifdef:**、  **\#Else**、  **\#Endif**次のコード例として構築します。示しています。

```cpp
#Ifdef: NewParserVersion
*%   Use new preprocessor directives if the parser supports them.
*%   Lock out this entire code path by changing the prefix.
      #SetPPPrefix: #New_
      #New_PreCompiled: ...
      *%  Actually might use a mixture of old and new directives!
      #New_UndefinePrefix:
#Else:
*%  Otherwise only use the original set of directives.
      #OldDirectives: ...
#Endif:
```

さらに、プリプロセッサのプレフィックスが間に設定する別のもの新しいディレクティブ分岐を実行しています。 パーサーは、不適切なプレフィックスを持つディレクティブが発生したかどうかに警告されます。

 

 




