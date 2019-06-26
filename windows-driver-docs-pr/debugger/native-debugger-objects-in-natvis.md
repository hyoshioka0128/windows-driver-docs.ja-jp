---
title: NatVis のネイティブ デバッガー オブジェクト
description: Dx コマンドでは、NatVis の拡張機能モデルを使用して、C++ の式が表示されます。 NatVis の詳細については、デバッガーでのネイティブ オブジェクトのカスタム ビューの作成を参照してください。
keywords:
- NatVis 内のオブジェクトをネイティブ デバッガー"
ms.date: 08/10/2017
ms.localizationpriority: medium
ms.openlocfilehash: 652481c6f8c329c3ff45eea74cbe2f662046def5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366458"
---
# <a name="native-debugger-objects-in-natvis"></a>NatVis のネイティブ デバッガー オブジェクト

## <a name="overview"></a>概要

ネイティブ デバッガー オブジェクトは、さまざまな構成要素とデバッガー環境の動作を表します。 デバッガー オブジェクトの例では、次に示します。

-   セッション
-   スレッド/スレッド
-   プロセス/処理
-   スタック フレームのスタック フレーム/
-   ローカル変数
-   モジュール/モジュール
-   ユーティリティ
-   状態
-   設定

デバッガー オブジェクトとの対話には、dx コマンドと LINQ を使用できます。 詳細については、次を参照してください。 [dx (表示デバッガー オブジェクト モデルの式)](dx--display-visualizer-variables-.md)と[デバッガー オブジェクトで LINQ を使用して](using-linq-with-the-debugger-objects.md)します。

JavaScript を使用してデバッガー オブジェクトを操作することもできます。 詳細については、「その[JavaScript 拡張機能のネイティブ デバッガー オブジェクト](native-objects-in-javascript-extensions.md)します。

このトピックでは、デバッガー オブジェクトを表示するカスタムの NatVis ビジュアライザーを作成する方法について説明します。 

## <a name="natvis-development-resources"></a>NatVis 開発リソース

これらのリソースの NatVis の使用に関する一般的な情報を参照してください。

[ネイティブ オブジェクトのカスタム ビューを作成します。](https://docs.microsoft.com/visualstudio/debugger/create-custom-views-of-native-objects?view=vs-2015)

[.Natvis ファイルを使用して C++ のデバッガーの種類のビジュアライザーを書き込み](https://code.msdn.microsoft.com/windowsdesktop/Writing-type-visualizers-2eae77a2)

[ **.nvload**](-nvload--natvis-load-.md)

[ **.nvlist**](-nvlist--natvis-list-.md)

[ **.nvunload**](-nvunload--natvis-unload-.md)

[ **.nvunloadall**](-nvunloadall--natvis-unload-all-.md)


## <a name="span-idcustomnatvisobjectexamplespanspan-idcustomnatvisobjectexamplespanspan-idcustomnatvisobjectexamplespancustom-natvis-object-example"></a><span id="Custom_NatVis_object_example"></span><span id="custom_natvis_object_example"></span><span id="CUSTOM_NATVIS_OBJECT_EXAMPLE"></span>カスタムの NatVis オブジェクトの例


クラスのインスタンスがある単純な C++ アプリケーション作成**CDog**します。

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

この XML を含む Dog.natvis という名前のファイルを作成します。

```XML
<?xml version="1.0" encoding="utf-8"?>
<AutoVisualizer xmlns="https://schemas.microsoft.com/vstudio/debugger/natvis/2010">
   <Type Name="CDog">
      <DisplayString>{{Age = {m_age} years. Weight = {m_weight} pounds.}}</DisplayString>
   </Type>
</AutoVisualizer>
```

Windows のツールのデバッグのビジュアライザー フォルダーのインストール ディレクトリに Dog.natvis をコピーします。 以下に例を示します。

C:\\プログラム ファイル\\(x64) の Windows 用デバッグ ツール\\ビジュアライザー

プログラムを実行し、main 関数に分割します。 ステップを実行できるように、変数`MyDog`が初期化されます。 表示`MyDog`を使用して[**いますか。** ](----evaluate-c---expression-.md) 使用してもう一度と**dx**します。

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


## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。

[dx (表示デバッガー オブジェクト モデルの式)](dx--display-visualizer-variables-.md)

[デバッガー オブジェクトを LINQ で使用します。](using-linq-with-the-debugger-objects.md)

[JavaScript の拡張機能のネイティブ デバッガー オブジェクト](native-objects-in-javascript-extensions.md) 

 
---
 






