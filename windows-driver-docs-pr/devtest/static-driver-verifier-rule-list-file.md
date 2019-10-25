---
title: 静的ドライバー検証規則リストファイル
description: 静的ドライバー検証規則リストファイル
ms.assetid: 941df64c-b66b-4e7b-b340-9ef6b57d895d
keywords:
- 静的ドライバー検証ツール WDK、入力ファイル
- StaticDV WDK、入力ファイル
- SDV WDK、入力ファイル
- 入力ファイル WDK 静的ドライバー検証ツール
- ファイル WDK 静的ドライバーの検証ツール
- 規則 WDK 静的ドライバー検証ツール
- 規則リストファイル WDK 静的ドライバー検証ツール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b65b925b8d6c87bafb0bcb7a7ac877efa54035fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839308"
---
# <a name="static-driver-verifier-rule-list-file"></a>静的ドライバー検証規則リストファイル


SDV ルールリストファイルは、1つまたは複数の[静的ドライバ検証ルール](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)またはルール名パターンを一覧表示するテキストファイルで、各行に1つのルールまたはルール名パターンが含まれています。 規則は任意の順序で表示でき、表示される順序で検証されます。 ファイルには、sdv などのファイル名拡張子が付いています。

各行に記載されているルールには、1つのルールの名前を指定することも、すべての SDV ルールを表すワイルドカード文字 (\*) を指定することもできます。

SDV には、\\ツール\\SDV\\サンプルの一連の便利な規則リストファイルが含まれています。\\規則\_設定すると、WDK の wdm サブディレクトリ\\設定され、独自のサブディレクトリを作成できます。

コマンドで規則の一覧ファイルを使用するには、「[静的ドライバーの検証コマンド (MSBuild)](-static-driver-verifier-commands--msbuild-.md)」を参照してください。

通常は、ルールの一覧ファイルを使用して、ルール名パターンで指定できない SDV 検証の複数のルールを指定します。 また、バッチと回帰のテストにも役立ちます。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

次のサンプルルール一覧ファイルは、選択した SDV ルールのセットを一覧表示します。

```
AddDevice
IrqlApcLte
LowerDriverReturn
KeWaitDeadlock
ZwRegistryOpen
```

次のコマンドでは、ルールリストファイル MyRules. sdv を使用して SDV 検証を開始します。

```
msbuild /t:sdv /p:Inputs="/check:D:\SDV\MyRules.sdv" mydriver.VcxProj /p:Configuration="Windows 7 Release" /p:Platform=Win32
```

### <a name="span-idcommentspanspan-idcommentspancomment"></a><span id="comment"></span><span id="COMMENT"></span>関する

検証の規則を一覧表示するために作成する規則の一覧ファイルには、ファイル名拡張子として sdv が使用されています。 ルールの SDV ソースコードファイルには、slic ファイル名拡張子が付いています。

 

 





