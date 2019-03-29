---
title: カスタム データ型を定義する方法
description: カスタム データ型を定義する方法
ms.assetid: 849f83ae-5fe7-447b-9d02-3d980757bf7d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bb1889b4508fff579fbe6ca241c53363d0bde74
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578020"
---
# <a name="how-do-you-define-custom-data-types"></a>カスタム データ型を定義する方法


Event Tracing for Windows (ETW) トレース関数で使用するためのいくつかの単純および複雑な型を定義します。 これらの型は、Defaultwpp.ini ファイルで宣言されます。 ただし、独自のカスタム データ型を作成することができます。

変数を宣言し、--整数ではなく意味のある条項 - を使用して、変数の値を説明したい場合は、カスタム データ型を使用します。

たとえば、 *DiskState*変数には、ディスクの状態が含まれています。 値を次に*DiskState*:

```
DiskOffline = 0
DiskOnline = 1
DiskFailed = 2
DiskStalled = 3
```

読み取りではなく"DiskState = 2"、トレース メッセージの意味を検索しなくてで**2**と呼ばれるカスタム型を定義する*DiskState*「DiskState が失敗しました」と書かれたトレース メッセージを取得します。

### <a name="span-idcreatingacustomdatatypespanspan-idcreatingacustomdatatypespancreating-a-custom-data-type"></a><span id="creating_a_custom_data_type"></span><span id="CREATING_A_CUSTOM_DATA_TYPE"></span>カスタム データ型を作成します。

カスタム データ型を作成するには、次の手順を完了します。

1.  Localwpp.ini など、.ini のファイル名拡張子を持つローカル構成ファイルを作成します。 ヘッダーまたはソース ファイルにカスタム型を追加することはできません。

2.  TYPEMACRO 定数を使用すると、カスタム データ型を定義します。

3.  ソースまたはヘッダー ファイルで構成データを特定します。

4.  追加、 **- ini** 、実行するようにパラメーター\_WPP マクロで、ソース ファイル。

5.  トレース メッセージにカスタム データ型を使用します。

### <a name="span-iddefiningatypemacroconstantspanspan-iddefiningatypemacroconstantspandefining-a-typemacro-constant"></a><span id="defining_a_typemacro_constant"></span><span id="DEFINING_A_TYPEMACRO_CONSTANT"></span>TYPEMACRO 定数を定義します。

次の形式を持つ TYPEMACRO 定数を定義します。 値は、文字列のリストとして定義されます。

```
TYPEMACRO(Type,{ItemListLong | ItemListShort | ItemListByteShort | ItemListByteLong},(Value1,Value2...));
```

この場合

<span id="ItemListShort"></span><span id="itemlistshort"></span><span id="ITEMLISTSHORT"></span>**ItemListShort**  
符号付き 16 ビット整数。

<span id="ItemListLong"></span><span id="itemlistlong"></span><span id="ITEMLISTLONG"></span>**ItemListLong**  
符号付きまたは符号なし 32 ビット整数。

<span id="ItemSetByteShort"></span><span id="itemsetbyteshort"></span><span id="ITEMSETBYTESHORT"></span>**ItemSetByteShort**  
符号付き 16 ビットのビット値。

<span id="ItemSetByteLong"></span><span id="itemsetbytelong"></span><span id="ITEMSETBYTELONG"></span>**ItemSetByteLong**  
符号付きまたは符号なし 32 ビットのビット値。

例:

```
TYPEMACRO(DiskState,ItemListLong(DiskOffline,DiskOnline,DiskFailed,DiskStalled));
```

### <a name="span-ididentifyingtheconfigurationdataspanspan-ididentifyingtheconfigurationdataspanidentifying-the-configuration-data"></a><span id="identifying_the_configuration_data"></span><span id="IDENTIFYING_THE_CONFIGURATION_DATA"></span>構成データを識別します。

ソース ファイルやヘッダー ファイルなどの他のコードを含むファイルへのカスタム データ タイプを追加した場合を使用して、**開始\_wpp config**と**エンド\_wpp**ステートメントを識別するために、ファイル内のデータを構成します。 例:

```
// begin_wpp config
    //TYPEMACRO(DiskState,ItemListLong(DiskOffline,DiskOnline,DiskFailed,DiskStalled));
// end_wpp
```

ローカル構成ファイルにカスタム データ タイプを追加した場合、**開始\_wpp config**と**エンド\_wpp**ステートメントは必要ありません。

### <a name="span-idaddtheiniparameterspanspan-idaddtheiniparameterspanadd-the--ini-parameter"></a><span id="add_the__ini_parameter"></span><span id="ADD_THE__INI_PARAMETER"></span>-Ini パラメーターを追加します。

カスタム型のローカル構成ファイルを作成するときに追加する必要があります、 **- ini** 、実行するようにパラメーター\_WPP プリプロセッサを呼び出す WPP ステートメント。

**- Ini**パラメーターだけでなく Defaultwpp.ini を使用して構成ファイル (.ini) で構成データを検索する ETW に指示します。 例:

```
RUN_WPP -km -ini:localwpp.ini
```

> [!IMPORTANT]
> 指定する必要があります、 **km**実行で切り替える\_WPP ディレクティブのユーザー モード アプリケーションまたはダイナミック リンク ライブラリ (Dll)。

 

### <a name="span-idusingthecustomdatatypespanspan-idusingthecustomdatatypespanusing-the-custom-data-type"></a><span id="using_the_custom_data_type"></span><span id="USING_THE_CUSTOM_DATA_TYPE"></span>カスタム データ型の使用

カスタム データ型を定義した後は、トレース メッセージで使用することができます。 パーセント記号の型名の前 (**%**) と感嘆符 (!) で囲みます。 例:

```
DoTraceMessage(INFO,"Disk State is %!diskstate!",DiskState); 
```

結果のトレース メッセージは、値を表すために定義する定数を使用します。

```
DiskState is Offline.
```
