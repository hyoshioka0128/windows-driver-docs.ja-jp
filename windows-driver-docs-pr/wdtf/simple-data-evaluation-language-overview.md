---
title: Simple Data Evaluation Language の概要
description: WDTF には、属性またはリレーションシップに基づくターゲットを収集する場合のタスクを簡略化する単純なクエリ言語が含まれています。
ms.assetid: 84c2a1d6-6bec-4aeb-b858-c29f50d74390
keywords:
- Windows デバイスのテスト フレームワーク、WDK SDEL
- WDTF WDK、SDEL
- 単純なデータ評価言語 WDK WDTF
- SDEL WDK WDTF
- クエリ言語 WDK WDTF
- ターゲット オブジェクト WDK WDTF
- WDK WDTF 名前空間
- テストの WDK WDTF のリレーションシップに基づく
- 関係の指定子 WDK WDTF
- 名前付きクエリ WDK WDTF
- WDK WDTF 属性
- ブール ロジック WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4506c87e759b6978de5286b57035eb866795450
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369486"
---
# <a name="simple-data-evaluation-language-overview"></a>Simple Data Evaluation Language の概要


WDTF には、属性またはリレーションシップに基づくターゲットを収集する場合のタスクを簡略化する単純なクエリ言語が含まれています。 単純なデータ評価言語 (SDEL) は、XPath と似ています。 XPath の詳細については、次を参照してください。 [XPath リファレンス](https://go.microsoft.com/fwlink/p/?linkid=33165)します。

このトピックでは、次のセクションでは、SDEL を使用する方法について説明します。

**注**  名前空間のすべてのトークンとそれらに含まれる属性のトークンの一覧は、次を参照してください。 [SDEL トークン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

 

### <a name="sdel-syntax-basics"></a>SDEL 構文の基礎

SDEL では、トークンの属性を使用して、一致を実行し、データを取得します。 すべての SDEL トークンには、英数字とハイフン (-) のみを含めることができます。

*属性*をターゲットに接続されているデータを 1 つを参照します。 として、属性の実際の値が格納されている、**バリアント**します。 後ろに比較演算子を配置する場合、*テスト*SDEL、属性の後の値が比較の一致を実行します。 1 つのテスト値を配置する必要があります。 または二重引用符--この表記法では、実際一重または二重引用符の両方ではなく、テスト値を使用することができます。 場合テスト値は、英数字のみで構成され、ハイフン (-)、引用符を省略できます。

### <a name="comparison-operations"></a>比較演算

SDEL では、属性、トークンに従うさまざまな比較演算子を許可します。 比較時に、演算子の左側に属性の実際の値が行われたを通じて演算子の右側にテスト値の同じ型、 **VariantChangeType** (Microsoft に記載されているメソッドWindows SDK ドキュメント)。 次の表では、SDEL をサポートしている別の比較演算子を示します。

比較演算子の意味の等号 (=)

使用して比較されます、種類が変更された後、 **VarCmp**メソッド (これは、Windows SDK のドキュメントで説明されている)。

非等値 (! =)

より小さい (&lt;)

以下 (&lt;=)

大きい (&gt;)

大きいか等しい (&gt;=)

ビットごとの AND (&)

この演算子では、型を強制的に VT\_I8、実際のビットごとの AND およびテスト値を実行する前にします。

指定された比較操作はありません (と値はありません)

かどうか、属性の実際の値は型 VT\_BOOL、--はその値に基づいて、一致が満たされて、比較演算子を行う必要はありません"IsDisableable = True"です。 それ以外の場合、すべての任意の値がある場合 (VT 以外\_空)、一致が満たされています。

 

ある場合は、複数の実際の値 (または配列) 属性で、すべての比較演算子する必要があります、少なくとも 1 回、反対側に動作する非等値演算子以外に一致するように解釈されます。 場合は、型のすべての比較することはできません (つまり、 **VariantChangeType**が失敗した)、一致がない (を逆の動作を持つ非等値演算子を除く)。

### <a name="understanding-attribute-namespaces"></a>属性の名前空間について

SDEL 属性をグループ化の名前空間のトークンを使用します。 名前空間のすべてのトークンとそれらに含まれる属性のトークンの一覧は、次を参照してください。 [SDEL トークン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

ルート名前空間の外にあるすべての属性を使用するには、名前空間の名前とし、2 つのコロン (:) を持つ属性を付ける必要があります。 次の VBScript コード例では、Disk::IsRemovable 属性の値が表示されます。

```cpp
WScript.Echo "Is Removable?: " & DeviceObj.GetValue("Disk::IsRemovable")
```

### <a name="examining-a-target-by-using-getvalue-and-eval"></a>GetValue を使用して、評価版のターゲットを調べる

[ **IWDTFTarget2::GetValue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-getvalue)メソッドを使用して、その属性のターゲットを確認できます。 VBScript のコード例を次の値を表示する、 [FriendlyName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)ターゲットの属性。

```cpp
WScript.Echo "FriendlyName: " & Device.GetValue("FriendlyName")
```

トークンの属性の一覧については、次を参照してください。 [SDEL トークン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

使用することも、 [ **IWDTFTarget2::Eval** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-eval)ターゲットに対して、SDEL ステートメントを評価するメソッド。 **Eval**返します**バリアント\_TRUE**または**バリアント\_FALSE**します。 次の VBScript コード例では**Eval**デバイスを無効にするかどうかを判断します。

```cpp
If Device.Eval("IsDisableable=true") Then 
    WScript.Echo "Target is disableable!"
End If
```

使用することも[ **Eval** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-eval)属性の存在をテストします。 渡す場合**Eval**属性がない比較演算子または値、 **Eval**戻ります**バリアント\_TRUE**属性または名前空間は、任意の値 (を保持している場合他にも**VT\_空**)。 次の VBScript コード例では**Eval**にターゲット SymbolicLink キーワードがあるか。

```cpp
If Device.Eval("SymbolicLink") Then 
    WScript.Echo "Target has a SymbolicLink!"
End If
```

さらに、比較演算子がありませんが、含まれている属性を**VT\_BOOL**に適用される暗黙的な '= true' の比較をある値を指定します。 この暗黙的な比較は、"IsDisableable"と同じであることを意味"IsDisableable = 'true'"です。

### <a name="navigating-relationships"></a>リレーションシップのナビゲーション

多くの場合、テストするには、関連するデバイスの状態を変更するときの動作を確認する必要があります。 たとえば、USB ハブを無効にするの操作を行いますにアタッチされているデバイス状態の変更を適切に処理しますか。 さらに、関連するデバイスの情報に基づいたデバイスを検索する場合があります。 この機能をサポートするためには、SDEL には、任意の属性または名前空間の前に (ただし、それらのいずれかの後ではなく) 1 つまたは複数の論理リレーションシップを指定する方法が含まれています。 リレーションシップのトークンは、属性または名前空間からフォワード スラッシュ (/) で区切られます。 VBScript のコード例を次の値を表示する、 [FriendlyName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)ターゲットの親のデバイスの属性。

```cpp
WScript.Echo "FriendlyName: " & Device.GetValue("parent/FriendlyName")
```

リレーションシップの修飾子を組み合わせることもできます。 VBScript のコード例を次の値を表示する、 [FriendlyName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)ターゲット オブジェクトの祖父母デバイスの属性です。

```cpp
WScript.Echo "FriendlyName: " & Device.GetValue("parent/parent/FriendlyName")
```

場合によっては、デバイスは、多対多のリレーションシップを持ちます。 たとえば、論理記憶域ボリュームが多数の物理ディスクに存在する可能性があり、これらの個々 のディスクは、多数のボリュームに領域を投稿可能性があります。

WDTF、ファントム以外のすべてのデバイス内で (つまり、物理的に操作するデバイス) ルート デバイスの子孫 (から取得できますが、 [ **RootDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtfdevicedepot2-get_rootdevice)プロパティ)。 (ファントムのデバイスの詳細については、次を参照してください[WDTF シナリオの作成](creating-wdtf-scenarios.md)。)。

### <a name="collecting-targets-by-using-getrelations"></a>GetRelations を使用して、ターゲットの収集

次の図は、 [ **IWDTFTarget2::GetRelations** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-getrelations)メソッド。

![target::getrelations メソッドを示す図](images/wdtf-getrelations.gif)

[ **IWDTFTarget2::GetRelations** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-getrelations)メソッド SDEL ステートメントの構文の関係指定子の部分だけを受け取り、返します、 [ **IWDTFTargets2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtftargets2)を含むすべての関係の条件を満たすターゲット コレクションのインターフェイス。 次の VBScript コード例では、元のターゲットとその兄弟すべてを含むコレクションを返します。

```cpp
Set TestDevices = Device.GetRelations("parent/child/", "")
```

2 番目のパラメーターを[ **GetRelations** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-getrelations)に渡されるステートメントを含めることができます必要に応じて、 [ **Eval** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-eval)するメソッドをそれぞれ対象特定のリレーションシップを満たしています。 追加する場合など、 *IsDisableable = true* 2 番目のパラメーターとして、上記のコード例をデバイスのみと無効にできる、兄弟返すとします。

一致がない場合は、0 個の項目のコレクションが返されます。

### <a name="collecting-targets-by-using-query"></a>クエリを使用してターゲットの収集

[ **IWDTFDeviceDepot2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtfdevicedepot2)インターフェイスが含まれています、**クエリ**メソッド。 このメソッドは、SDEL ステートメント用に設計された、 [ **IWDTFTarget2::Eval** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-eval)メソッドの新しいインスタンスを返します、 [ **IWDTFTargets2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtftargets2)クエリの条件を満たすターゲットのサブセットを格納しているコレクションのインターフェイス。 次の VBScript コード例では、ファントム以外のすべてのデバイスを列挙し、各デバイスのフレンドリ名を示します。

```cpp
For Each Device In WDTF.DeviceDepot.Query("IsPhantom=false")
    WScript.Echo Device.GetValue("FriendlyName")
Next
```

返されるコレクションには、 [ **IWDTFTargets2::Query** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftargets2-query)メソッド、同一の実装に**IWDTFDeviceDepot2::Query**。 **IWDTFTargets2::Query** SDEL ステートメントに一致する元のコレクションからターゲットのサブセットを返します。

### <a name="boolean-logic-in-sdel"></a>SDEL でブール ロジック

[ **IWDTFTarget2::GetRelations** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-getrelations)メソッドがブール値のみを受け入れる**または**演算子が、呼び出しを[ **IWDTFTargets2:。クエリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftargets2-query)、 [ **IWDTFTarget2::Eval**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-eval)、および[ **IWDTFTarget2::GetValue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-getvalue)メソッドはブール値を使用できます**AND**と**または**演算子。 **クエリ**メソッドと**Eval**メソッド、演算子は通常のブール演算子を予想どおりの結果を返すように動作します。 ただし、 **GetValue**メソッド、 **AND**自体の両方の側で値を構成し、**または**(左から開始) が見つかった最初の値のみが返されます。

### <a name="parentheses-in-sdel"></a>SDEL 内のかっこ

SDEL のすべてのステートメントでは、かっこを使用して、ブール ロジックの評価順序を指定します。 リレーションシップまたは名前空間の下のステートメントで、サブ要素をグループ化かっこを使用することもできます。

次の VBScript コード例では、すべてのボリュームと親の親のデバイスの子を取得します。

```cpp
Set Devices = Device.GetRelations("parent/parent/(child/ OR volume/)", "")
```

次の VBScript コード例をリムーバブル メディアを 1,000,000 バイトを超えるを持つ子を持つすべてのデバイスを取得します。

```cpp
Set Devices = WDTF.DeviceDepot.Query("child/disk::(IsRemovable=true AND Size>1000000)")
```

### <a name="sdel-syntax-parsing"></a>SDEL 構文の解析

WDTF メソッドのいずれかに、SDEL ステートメントに無効な構文を渡すと、メソッドは失敗し、詳細なエラー情報が返され、問題について説明します。

**注**  スペル ミスの属性、名前空間、または関係トークン エラーは発生しません、構文、ため SDEL は動的であるターゲットに基づいて設計されています。SDEL ステートメントは、動的フィールドのセット内の属性が存在するクエリを実行できる必要があります。

 

 

 




