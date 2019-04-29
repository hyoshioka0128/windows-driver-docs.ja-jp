---
title: 無効な GDL 構成の使用
description: 無効な GDL 構成の使用
ms.assetid: a61232dd-ab64-4ca4-9eb9-68fe5c7249e4
keywords:
- GDL WDK の構成
- WDK GDL、無効な構成の構成
- 無効な GDL 構成 WDK
- WDK GDL、例の構成
- InvalidCombination ディレクティブ WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1226ffd071ea12c837db07467e22700111368188
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387130"
---
# <a name="using-invalid-gdl-configurations"></a>無効な GDL 構成の使用


すべての可能な構成が有効で許可されています。 たとえば、印刷デバイスには、一杯やるメディア、メディアが詰まり可能性がありますので、どの入力トレイに配置する場合がありますできません。 GDL 言語では、無効なパラメーター設定の組み合わせを定義することでも無効な構成を定義することができます。

\*InvalidCombination ディレクティブは、この目的のために使用します。 値\*InvalidCombination は同時に使用できない 2 つ以上のパラメーターの設定の名前を示す一覧です。 パラメーターの設定を指定するために使用する構文は、EBNF の表記で、次のコード例に示すようです。

```cpp
InvalidCombination_Directive :== "*InvalidCombination" S ":"  S ParamSettingsList  S LB
ParamSettingsList :== "LIST" S "("  S ParamSetting S ","  S ParamSetting ( S "," S ParamSetting)?  S ")"
ParamSetting :== ParameterName "." Value
ParameterName :== {Construct Tag of *Feature construct}
Value :==  {Construct Tag of *Option construct found within the *Feature construct.}
S :== [#x20#x09]*
LB :== [#x0A] | [#x0D] | ([#x0A] [#x0D]) | ([#x0D] [#x0A])
```

\*InvalidCombination ディレクティブが GDL ファイルのルート コンテキストで表示する必要があります。

たとえば週末に雨を回避したい場合は、次のコードを指定できます。

```cpp
*InvalidCombination: LIST(Weather.Rain, Today.Saturday)
*InvalidCombination: LIST(Weather.Rain, Today.Sunday)
```

正常な状態にした場合にのみ、週末に雨を回避したい場合は、次のコードを指定できます。

```cpp
*InvalidCombination: LIST(Weather.Rain, Today.Saturday, Health.Well)
*InvalidCombination: LIST(Weather.Rain, Today.Sunday, Health.Well)
```

\*InvalidCombination ディレクティブは、上記のコード例では、(Weather.Rain、Today.Sunday、Health.Well または Weather.Rain、Today.Saturday、Health.Well) は、特定の組み合わせを含む任意の構成に違反していることを指定します、ディレクティブ。

\*InvalidCombination ディレクティブは、特定の種類の制約。 GDL パーサー関数は、指定された構成が続行する前に、GDL ファイルで定義されている制約のいずれかに違反しているを確認します。 違反が検出された場合、構成が変更された (または解決)、制約に違反しないようにします。 このような状況と呼ばれる[制約を解決する](resolving-gdl-configuration-conflicts.md)します。 何百も数十個のパラメーターに関連する制約の 1 つ GDL ファイルに存在します。 制約は、1 つのパラメーターの設定の変更では、その他のパラメーターで、連鎖的に変更が生じるように相互作用の複雑な web を形成できます。

**注**  既定の構成にすべての制約に違反していないことを確認する必要があります。 その場合、パーサー インターフェイスの関数のいずれもは成功します。

 

**注**   、GDL パーサーでは、特殊なケースもが受け入れる\*InvalidCombination だけ 2 つのパラメーター設定を含むです。

 

 

 




