---
title: WinDbg Preview - Scripting メニュー
description: このセクションでは、WinDbg プレビュー デバッガーでスクリプトを使用する方法について説明します。
ms.date: 04/10/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45b2b80bf9d3514ca9bdc11a0d8c657518791c16
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353061"
---
# <a name="windbg-preview---scripting"></a>WinDbg Preview - Scripting 

このセクションでは、WinDbg プレビューでスクリプトのサポートを使用する方法について説明します。

![スクリプト デバッガー メニューのスクリーン ショット](images/windbgx-javascript-new-script.png)

プレビューの WinDbg スクリプト ウィンドウの基本的な構文の強調表示、IntelliSense、およびエラーの認識機能します。 

リボンのボタンを使用します。
- 新しいスクリプトを作成します。 
- 既存のスクリプトを開く
- スクリプトを実行します。
- スクリプトを保存します。 
- スクリプトのリンクを解除します。
- JavaScript のプロバイダーを読み込む

スクリプト ウィンドウで右クリックして、スクリプトを実行することができますも自動的に*スクリプトの実行で保存*します。 スクリプトを正常に読み込むと、緑色のチェック ボックスは、スクリプトのタイトル バーに表示されます。 スクリプトでエラーがある場合は赤い x が表示されます。

## <a name="javascript-scripting"></a>JavaScript スクリプト 

JavaScript を使用するには、する必要がありますまずするデバッグ ターゲット。 JavaScript での作業を開始する準備ができたら、"負荷 JavaScript Provider"をクリックします。 その後、これらの 2 種類のスクリプト テンプレートを選択して、新しい JavaScript を作成できます。

- **拡張機能のスクリプト**-スクリプトは、デバッガーの拡張機能として機能するように設計されています。  デバッガーのオブジェクト モデルを操作して、継続的な機能を提供します。  なるもののアクションが行われない、 <i>Execute</i>リボンのボタンをクリックします。

- **スクリプトの命令型**-は、毎回アクションを実行できるように設計されたスクリプト、 <i>Execute</i>リボンのボタンをクリックします。 このようなスクリプトは、デバッガーのオブジェクト モデルを一般には変更されません。

JavaScript の使用に関する詳細については、これらのトピックを参照してください。

[JavaScript デバッガー スクリプト](javascript-debugger-scripting.md)

[JavaScript の拡張機能のネイティブ デバッガー オブジェクト](native-objects-in-javascript-extensions.md)

[JavaScript デバッガーの スクリプトの例](javascript-debugger-example-scripts.md)

## <a name="natvis-scripting"></a>NatVis Scripting 

使用**新しいスクリプト** > **NatVis**を次の空の NatVis テンプレートを開きます。

```xml
<AutoVisualizer xmlns="https://schemas.microsoft.com/vstudio/debugger/natvis/2010">
  <Type Name="">
  </Type>
</AutoVisualizer>
```

NatVis の使用方法の詳細については、次を参照してください。[に NatVis デバッガー オブジェクト](native-debugger-objects-in-natvis.md)します。

 
---

## <a name="see-also"></a>関連項目

[WinDbg のプレビューを使用したデバッグ](debugging-using-windbg-preview.md)

 





