---
title: WinDbg プレビュー-[スクリプト] メニュー
description: このセクションでは、WinDbg preview デバッガーでスクリプトを使用する方法について説明します。
ms.date: 01/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: baa6478da0d8cd1d0ff3c0a74c3fc24fa6ce67c2
ms.sourcegitcommit: 6d930ed810124ade8e29a617c7abcd399113696f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2020
ms.locfileid: "76256667"
---
# <a name="windbg-preview---scripting-menu"></a>WinDbg プレビュー-[スクリプト] メニュー

このセクションでは、WinDbg プレビューでスクリプトのサポートを使用する方法について説明します。

![デバッガーのスクリプト作成メニューのスクリーン ショット](images/windbgx-javascript-new-script.png)

[WinDbg Preview スクリプト] ウィンドウには、基本的な構文の強調表示、IntelliSense、およびエラー認識機能があります。 

リボンのボタンを使用して、次のことを行います。
- 新しいスクリプトを作成する
- 既存のスクリプトを開く
- スクリプトの実行
- スクリプトを保存する 
- スクリプトのリンク解除

スクリプトウィンドウを右クリックし、 *[保存時にスクリプトを実行*] を選択して、スクリプトを自動的に実行することもできます。 スクリプトを正常に読み込むと、スクリプトのタイトルバーに緑色のチェックボックスが表示されます。 スクリプトにエラーがある場合は、赤い x が表示されます。

## <a name="javascript-scripting"></a>JavaScript スクリプト

JavaScript の使用を開始するには、まずターゲットをデバッグする必要があります。 JavaScript での作業を開始する準備ができたら、[JavaScript プロバイダーの読み込み] をクリックします。 その後、この2種類のスクリプトテンプレートを選択することで、新しい JavaScript を作成できます。

- **拡張スクリプト**-デバッガーの拡張機能として機能するように設計されたスクリプトです。  デバッガーのオブジェクトモデルを操作し、継続的な機能を提供します。  リボンの [<i>実行</i>] ボタンをクリックしてもアクションは発生しません。

- **命令型スクリプト**-リボンの [<i>実行</i>] ボタンがクリックされるたびにアクションを実行するように設計されたスクリプトです。 このようなスクリプトでは、通常、デバッガーのオブジェクトモデルは変更されません。

JavaScript の使用方法の詳細については、次のトピックを参照してください。

[JavaScript デバッガー スクリプト](javascript-debugger-scripting.md)

[JavaScript 拡張機能のネイティブデバッガーオブジェクト](native-objects-in-javascript-extensions.md)

[JavaScript デバッガーのサンプルスクリプト](javascript-debugger-example-scripts.md)

## <a name="natvis-scripting"></a>NatVis スクリプト 

**新しいスクリプト** > **NatVis**を使用して、次の空の NatVis テンプレートを開きます。

```xml
<AutoVisualizer xmlns="https://schemas.microsoft.com/vstudio/debugger/natvis/2010">
  <Type Name="">
  </Type>
</AutoVisualizer>
```

NatVis の操作の詳細については、「 [NatVis のデバッガーオブジェクト](native-debugger-objects-in-natvis.md)」を参照してください。

 
---

## <a name="see-also"></a>関連項目

[WinDbg プレビューを使用したデバッグ](debugging-using-windbg-preview.md)
