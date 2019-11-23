---
title: Simple Data Evaluation Language の概要
description: WDTF には、属性または関係に基づいてターゲットを収集するタスクを簡略化する単純なクエリ言語が用意されています。
ms.assetid: 84c2a1d6-6bec-4aeb-b858-c29f50d74390
keywords:
- Windows デバイステストフレームワーク WDK、SDEL
- WDTF WDK、SDEL
- Simple Data 評価言語 WDK WDTF
- SDEL WDK WDTF
- クエリ言語 WDK WDTF
- ターゲットオブジェクト WDK WDTF
- 名前空間 WDK WDTF
- リレーションシップベースのテスト WDK WDTF
- リレーションシップ指定子 WDK WDTF
- 名前付きクエリの WDK WDTF
- 属性 WDK WDTF
- ブール型ロジック WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc9d156518f931d1cb7c948a598d03cf36e6e652
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845269"
---
# <a name="simple-data-evaluation-language-overview"></a>Simple Data Evaluation Language の概要


WDTF には、属性または関係に基づいてターゲットを収集するタスクを簡略化する単純なクエリ言語が用意されています。 Simple Data 評価言語 (SDEL) は XPath に似ています。 XPath の詳細については、「 [Xpath リファレンス](https://go.microsoft.com/fwlink/p/?linkid=33165)」を参照してください。

このトピックの次のセクションでは、SDEL の使用方法について説明します。

**注**  すべての名前空間トークンとその中の属性トークンの一覧については、「 [sdel トークン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

 

### <a name="sdel-syntax-basics"></a>SDEL 構文の基本

SDEL は、属性トークンを使用して一致を実行し、データを取得します。 すべての SDEL トークンには、英数字とハイフン (-) のみを含めることができます。

*属性*は、ターゲットにアタッチされているデータを参照します。 属性の実際の値は、**バリアント**として格納されます。 属性の後に比較演算子の後に*テスト*値を配置すると、sdel は比較一致を実行します。 テスト値は一重引用符または二重引用符で囲む必要があります。この表記により、テスト値では実際の単一引用符または二重引用符を使用できますが、両方を使用することはできません。 テスト値が英数字とハイフン (-) のみで構成されている場合は、引用符を省略できます。

### <a name="comparison-operations"></a>比較操作

SDEL では、さまざまな比較演算子が属性トークンに従うことができます。 比較の時点で、演算子の左側にある属性の実際の値は、 **VariantChangeType**メソッド (Microsoft Windows SDK のドキュメントで説明されています) を使用して、演算子の右側にあるテスト値と同じ型になります。 次の表は、SDEL がサポートするさまざまな比較演算子を示しています。

比較演算子の意味等値 (=)

型が変更された後は、 **Varcmp** (Windows SDK のドキュメントで説明されている) メソッドを使用して比較されます。

不等号 (! =)

より小さい (&lt;)

以下 (&lt;=)

より大きい (&gt;)

以上 (&gt;=)

ビットごとの AND (&)

この演算子は、実際の値とテスト値のビットごとの AND を実行する前に、型を VT\_I8 に強制します。

比較演算 (および値なし) が指定されていません

属性の実際の値が VT\_BOOL 型の場合、その値に基づいて一致が満たされます。つまり、"IsDisableable = True" を実行するための比較演算子は必要ありません。 それ以外の場合、すべての値 (VT\_EMPTY 以外) がある場合は、一致が満たされます。

 

属性に複数の実際の値 (または配列) がある場合、逆の動作を持つ非等値演算子を除き、すべての比較演算子が少なくとも1つに一致するように解釈される必要があります。 型を比較できない (つまり、 **VariantChangeType**が失敗した) 場合、一致するものはありません (逆の動作を持つ非等値演算子を除きます)。

### <a name="understanding-attribute-namespaces"></a>属性の名前空間について

SDEL では、属性をグループ化するために名前空間トークンを使用します。 すべての名前空間トークンとその中の属性トークンの完全な一覧については、「 [Sdel トークン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

ルート名前空間の外部にある属性を使用するには、属性の先頭に名前空間名と2つのコロン (::) を付ける必要があります。 次の VBScript コード例では、Disk:: IsRemovable 属性の値を表示します。

```cpp
WScript.Echo "Is Removable?: " & DeviceObj.GetValue("Disk::IsRemovable")
```

### <a name="examining-a-target-by-using-getvalue-and-eval"></a>GetValue と Eval を使用したターゲットの検査

[**IWDTFTarget2:: GetValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-getvalue)メソッドを使用すると、その属性についてターゲットに要求できます。 次の VBScript コード例では、ターゲットの[FriendlyName](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)属性の値を出力します。

```cpp
WScript.Echo "FriendlyName: " & Device.GetValue("FriendlyName")
```

属性トークンの完全な一覧については、「 [Sdel トークン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

[**IWDTFTarget2:: Eval**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-eval)メソッドを使用して、ターゲットに対して sdel ステートメントを評価することもできます。 **Eval**は**variant\_TRUE**または**variant\_FALSE**を返します。 次の VBScript コード例では、 **Eval**を使用して、デバイスを無効にできるかどうかを判断します。

```cpp
If Device.Eval("IsDisableable=true") Then 
    WScript.Echo "Target is disableable!"
End If
```

また、 [**Eval**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-eval)を使用して、属性が存在するかどうかをテストすることもできます。 Eval は、属性または名前空間に ( **VT\_EMPTY**以外の) 値が保持されている場合**に、属性**を**評価**するときに、比較演算子または値を指定せずに、**バリアント\_TRUE**を返します。 次の VBScript コード例では、 **Eval**を使用して、ターゲットに SymbolicLink キーワードがあるかどうかを判断します。

```cpp
If Device.Eval("SymbolicLink") Then 
    WScript.Echo "Target has a SymbolicLink!"
End If
```

また、比較演算子がないが、 **VT\_BOOL**値を含む属性には、暗黙的な ' = true ' 比較が適用されます。 この暗黙的な比較は、"IsDisableable" が "IsDisableable = ' true '" と同じであることを意味します。

### <a name="navigating-relationships"></a>リレーションシップのナビゲート

多くの場合、テストでは、関連するデバイスの状態が変化したときの動作を調べる必要があります。 たとえば、USB ハブが無効になっている場合、そのハブに接続されているデバイスは、状態の変更を適切に処理しますか。 また、関連するデバイスの情報に基づいてデバイスを検索することもできます。 この機能をサポートするために、SDEL には、属性または名前空間の前に1つ以上の論理リレーションシップを指定する方法が含まれています (その後は除く)。 リレーショントークンは、スラッシュ (/) で属性または名前空間から分離されます。 次の VBScript コード例では、ターゲットの親デバイスの[FriendlyName](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)属性の値を出力します。

```cpp
WScript.Echo "FriendlyName: " & Device.GetValue("parent/FriendlyName")
```

また、リレーション修飾子を組み合わせることもできます。 次の VBScript コード例では、ターゲットオブジェクトの親デバイスの[FriendlyName](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)属性の値を出力します。

```cpp
WScript.Echo "FriendlyName: " & Device.GetValue("parent/parent/FriendlyName")
```

場合によっては、デバイスには多対多の関係があります。 たとえば、論理記憶域ボリュームが多数の物理ディスク上に存在し、それらの個々のディスクが多くのボリュームに領域を使用する場合があります。

WDTF 内では、すべての非ファントムデバイス (つまり、物理的に存在するデバイス) は、ルートデバイスの子孫です ( [**rootdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtfdevicedepot2-get_rootdevice)プロパティから取得できます)。 (ファントムデバイスの詳細については、「 [WDTF シナリオの作成](creating-wdtf-scenarios.md)」を参照してください)。

### <a name="collecting-targets-by-using-getrelations"></a>GetRelations を使用したターゲットの収集

次の図は、 [**IWDTFTarget2:: GetRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-getrelations)メソッドを示しています。

![target:: getrelations メソッドを示す図](images/wdtf-getrelations.gif)

[**IWDTFTarget2:: GetRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-getrelations)メソッドは、sdel ステートメント構文のリレーションシップ指定子部分のみを受け取り、リレーションシップ条件を満たすすべてのターゲットを含む[**IWDTFTargets2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftargets2) collection インターフェイスを返します。 次の VBScript コード例は、元のターゲットとそのすべての兄弟を含むコレクションを返します。

```cpp
Set TestDevices = Device.GetRelations("parent/child/", "")
```

[**Getrelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-getrelations)の2番目のパラメーターには、必要に応じて、特定のリレーションシップを満たす各ターゲットの[**Eval**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-eval)メソッドに渡すステートメントを含めることができます。 たとえば、2番目のパラメーターとして*Isdisableable = true*を追加した場合、上記のコード例では、無効にできるデバイスとその兄弟だけが返されます。

一致する項目がない場合は、項目が0のコレクションが返されます。

### <a name="collecting-targets-by-using-query"></a>クエリを使用したターゲットの収集

[**IWDTFDeviceDepot2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtfdevicedepot2)インターフェイスには、**クエリ**メソッドが含まれています。 このメソッドは、 [**IWDTFTarget2:: Eval**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-eval)メソッド用にデザインされた sdel ステートメントを受け取り、クエリの条件を満たすターゲットのサブセットを含む[**IWDTFTargets2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftargets2) collection インターフェイスの新しいインスタンスを返します。 次の VBScript コード例では、すべてのファントム以外のデバイスを列挙し、各デバイスのフレンドリ名を表示します。

```cpp
For Each Device In WDTF.DeviceDepot.Query("IsPhantom=false")
    WScript.Echo Device.GetValue("FriendlyName")
Next
```

返されるコレクションには、 **IWDTFDeviceDepot2:: query**と同じ実装を持つ[**IWDTFTargets2:: query**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftargets2-query)メソッドがあります。 **IWDTFTargets2:: Query**は、sdel ステートメントを満たす元のコレクションからターゲットのサブセットを返します。

### <a name="boolean-logic-in-sdel"></a>SDEL のブール型ロジック

[**IWDTFTarget2:: GetRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-getrelations)メソッドはブール型の**or**演算子のみを受け取ることができますが、 [**IWDTFTargets2:: Query**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftargets2-query)、 [**IWDTFTarget2:: Eval**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-eval)、および[**IWDTFTarget2:: GetValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-getvalue)の各メソッドの呼び出しでは **、ブール型の and 演算子**と**OR**演算子を使用できます。 **クエリ**メソッドと**Eval**メソッドでは、演算子は通常のブール演算子と同じように動作し、結果が期待どおりに返されます。 ただし、 **GetValue**メソッドの場合は、**と**がそれ自体の両側で値を構成します。**または**、が見つかった最初の値 (左側から) のみを返します。

### <a name="parentheses-in-sdel"></a>SDEL のかっこ

すべての SDEL ステートメントでは、かっこを使用して、ブール型ロジックの評価順序を指定できます。 また、かっこを使用して、リレーションまたは名前空間の下のステートメントでサブ要素をグループ化することもできます。

次の VBScript コード例では、親デバイスのすべてのボリュームと子を取得します。

```cpp
Set Devices = Device.GetRelations("parent/parent/(child/ OR volume/)", "")
```

次の VBScript コード例では、100万バイトを超えるリムーバブルメディアを持つ子を持つすべてのデバイスを取得します。

```cpp
Set Devices = WDTF.DeviceDepot.Query("child/disk::(IsRemovable=true AND Size>1000000)")
```

### <a name="sdel-syntax-parsing"></a>SDEL 構文の解析

無効な構文の SDEL ステートメントを WDTF 内のいずれかのメソッドに渡した場合、メソッドは失敗し、詳細なエラー情報が返されて問題が説明されます。

  **注**: 属性、名前空間、または関係トークンのスペルが間違っていると、構文エラーは発生しません。 sdel はターゲットに基づいて動的に設計されているため、sdel ステートメントは動的なフィールドセットに属性が存在するかどうかをクエリできる必要があります。

 

 

 




