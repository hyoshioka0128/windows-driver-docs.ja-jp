---
title: 静的ドライバー検証ツールの規則一覧ファイル
description: 静的ドライバー検証ツールの規則一覧ファイル
ms.assetid: 941df64c-b66b-4e7b-b340-9ef6b57d895d
keywords:
- Static Driver Verifier WDK、入力ファイル
- StaticDV WDK では、入力ファイル
- SDV の WDK、入力ファイル
- 入力ファイル WDK Static Driver Verifier
- WDK Static Driver Verifier のファイル
- WDK Static Driver Verifier の規則
- 規則の一覧ファイルの WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa8da1ae137057ab2f609acf2edb7f919c6246e6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365165"
---
# <a name="static-driver-verifier-rule-list-file"></a>静的ドライバー検証ツールの規則一覧ファイル


SDV ルールの一覧ファイルは、1 つまたは複数を一覧表示するテキスト ファイル[Static Driver Verifier ルール](https://msdn.microsoft.com/library/windows/hardware/ff551714)または名前パターンの 1 つのルールまたはルール名のパターンを行ごとに、ルールします。 ルールは任意の順序で表示でき、出現する順序で確認されています。 ファイルは、Test.sdv など、.sdv のファイル名拡張子を持ちます。

行ごとに表示されているルールは、1 つの規則の名前を指定できますか、ワイルドカード文字であることができます (\*)、すべての SDV のルールを表します。

SDV にはで便利なルールの一覧ファイルのセットが含まれています、\\ツール\\sdv\\サンプル\\ルール\_設定\\WDK の wdm サブディレクトリが独自作成できます。

コマンドで、ルールの一覧ファイルを使用する、次を参照してください。、 [Static Driver Verifier のコマンド (MSBuild)](-static-driver-verifier-commands--msbuild-.md)します。

通常、ルールの一覧のファイルは使用してルール名のパターンで指定することはできません SDV 検証のための複数のルールを指定します。 バッチおよび回帰テストに便利です。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

次のルール一覧ファイルの例では、SDV の選択した規則のセットを一覧表示します。

```
AddDevice
IrqlApcLte
LowerDriverReturn
KeWaitDeadlock
ZwRegistryOpen
```

次のコマンドは、SDV 検証を開始するのに、規則の一覧ファイル MyRules.sdv を使用します。

```
msbuild /t:sdv /p:Inputs="/check:D:\SDV\MyRules.sdv" mydriver.VcxProj /p:Configuration="Windows 7 Release" /p:Platform=Win32
```

### <a name="span-idcommentspanspan-idcommentspancomment"></a><span id="comment"></span><span id="COMMENT"></span>コメント

確認にルールを一覧表示を作成するルール一覧のファイルでは、.sdv のファイル名拡張子を持ちます。 ルールの SDV のソース コード ファイルでは、.slic ファイル名拡張子があります。

 

 





