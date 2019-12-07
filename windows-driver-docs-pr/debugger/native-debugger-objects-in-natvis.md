---
title: NatVis のネイティブ デバッガー オブジェクト
description: Dx コマンドは、NatVis C++拡張モデルを使用して式を表示します。 NatVis の詳細については、「デバッガーでのネイティブオブジェクトのカスタムビューの作成」を参照してください。
keywords:
- NatVis のネイティブデバッガーオブジェクト
ms.date: 08/10/2017
ms.localizationpriority: medium
ms.openlocfilehash: dced0a8dea51c87864447e104f9cf2ea3a82c742
ms.sourcegitcommit: 5a10ea8a98fa4b6f8c43176156530e859a71b10e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2019
ms.locfileid: "74908355"
---
# <a name="native-debugger-objects-in-natvis"></a>NatVis のネイティブ デバッガー オブジェクト

## <a name="overview"></a>概要

ネイティブデバッガーオブジェクトは、デバッガー環境のさまざまな構造と動作を表します。 デバッガーオブジェクトの例を次に示します。

-   セッション
-   スレッド/スレッド
-   プロセス/プロセス
-   スタックフレーム/スタックフレーム
-   ローカル変数
-   モジュール/モジュール
-   ユーティリティ
-   都道府県
-   設定

Dx コマンドと LINQ を使用して、デバッガーオブジェクトと対話することができます。 詳細については、「 [dx (デバッガーオブジェクトモデル式の表示)](dx--display-visualizer-variables-.md) 」および「[デバッガーオブジェクトでの LINQ の使用](using-linq-with-the-debugger-objects.md)」を参照してください。

JavaScript を使用して、デバッガーオブジェクトを操作することもできます。 詳細については、「 [JavaScript 拡張機能のネイティブデバッガーオブジェクト](native-objects-in-javascript-extensions.md)」を参照してください。

このトピックでは、カスタム NatVis ビジュアライザーを作成して、デバッガーオブジェクトを表示する方法について説明します。 

## <a name="natvis-development-resources"></a>NatVis 開発リソース

NatVis の使用に関する一般的な情報については、これらのリソースを参照してください。

[ネイティブ オブジェクトのカスタム ビューの作成](https://docs.microsoft.com/visualstudio/debugger/create-custom-views-of-native-objects?view=vs-2015)

[**nvload**](-nvload--natvis-load-.md)

[ **. nvlist**](-nvlist--natvis-list-.md)

[**nvunload**](-nvunload--natvis-unload-.md)

[ **.nvunloadall**](-nvunloadall--natvis-unload-all-.md)

## <a name="custom-natvis-object-example"></a>Custom NatVis オブジェクトの例

**Cdog**クラスC++のインスタンスを持つ単純なアプリケーションを作成します。

```cpp
class CDog
{
public:
   CDog(){m_age = 8; m_weight = 30;}
   long m_age;
   long m_weight;
};

int main()
{
   CDog MyDog;
   printf_s("%d, %d\n", MyDog.m_age, MyDog.m_weight);
   return 0;
}
```

次の XML を含む natvis という名前のファイルを作成します。

```XML
<?xml version="1.0" encoding="utf-8"?>
<AutoVisualizer xmlns="https://schemas.microsoft.com/vstudio/debugger/natvis/2010">
   <Type Name="CDog">
      <DisplayString>{{Age = {m_age} years. Weight = {m_weight} pounds.}}</DisplayString>
   </Type>
</AutoVisualizer>
```

Windows 用デバッグツールのインストールディレクトリの [ビジュアライザー] フォルダーに natvis をコピーします。 次に、例を示します。

C:\\プログラムファイル\\Windows 用デバッグツール (x64)\\ビジュアライザー

プログラムを実行し、main 関数で中断します。 変数 `MyDog` 初期化されるように手順を実行します。 ?? を使用して `MyDog` を表示し[**ますか**?](----evaluate-c---expression-.md) もう一度**dx**を使用します。

```dbgcmd
0:000> ??MyDog
class CDog
   +0x000 m_age        : 0n8
   +0x004 m_weight     : 0n30
0:000> *
0:000> dx -r1 MyDog
.....
MyDog     : {Age = 8 years. Weight = 30 pounds.} [Type: CDog]
```

## <a name="see-also"></a>関連項目

[dx (表示デバッガーオブジェクトモデル式)](dx--display-visualizer-variables-.md)

[デバッガーオブジェクトでの LINQ の使用](using-linq-with-the-debugger-objects.md)

[JavaScript 拡張機能のネイティブデバッガーオブジェクト](native-objects-in-javascript-extensions.md) 
