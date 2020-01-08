---
title: Windows Vista の新しいルート レベル専用 PPD 属性
description: Windows Vista の新しいルート レベル専用 PPD 属性
ms.assetid: 49cdfb2f-e119-4960-9e79-67e1025b753f
keywords:
- ルートレベルのみの属性 WDK Unidrv
- 一般的なプリンター属性 WDK Unidrv、ルートレベルのみ
- PPD 属性 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c28ea5fd3deaf50ce24b6f051ce344fc81b9373d
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75653020"
---
# <a name="new-root-level-only-ppd-attributes-for-windows-vista"></a>Windows Vista の新しいルート レベル専用 PPD 属性


次の一覧では、Windows Vista 以降で新しく追加された PPD 属性について説明します。 Windows Vista より前のバージョンの Windows との下位互換性を維持するには、これらの属性を次のコードで囲む必要があります。

```cpp
*Ifdef: WINNT_60 ... *Endif: WINNT_60 blocks
```

### <a name="msprintschemakeywordmap"></a>MSPrintSchemaKeywordMap

**MSPrintSchemaKeywordMap**属性は、ppd 機能キーワードからパブリック印刷スキーマ機能キーワードへのマッピング、または、ppd 機能の ppd オプションキーワードから、印刷スキーマ機能のパブリック出力スキーマオプションキーワードへのマッピングを定義します。

**MSPrintSchemaKeywordMap**には、次の2つの形式があります。

<a href="" id="format-1"></a>形式1  
```cpp
*MSPrintSchemaKeywordMap: PrintSchema_feature_keyword *<PPD_feature_keyword>
```

<a href="" id="format-2"></a>形式2  
```cpp
*MSPrintSchemaKeywordMap: PrintSchema_feature_keyword PrintSchema_option_keyword *<PPD_feature_keyword> <PPD_option_keyword>
```

両方の形式で、PPD 機能キーワードプレフィックス (アスタリスク \[\*\]) が必要です。

形式 1:

-   PPD 機能キーワードは、以前の PPD ファイルコンテンツで既に定義されている PPD 機能を参照する必要があります。

-   同じ PPD 機能の \***MSPrintSchemaKeywordMap**の複数の定義は許可されていません。 複数の定義が見つかった場合は、最初の定義のみが受け入れられ、他の定義は無視されます。

形式 2:

-   (Format 1 を使用した) PPD 機能の \***MSPrintSchemaKeywordMap**定義は、ppd 機能のオプションの \***MSPrintSchemaKeywordMap**定義が表示される前に存在している必要があります。

-   PPD オプションの \***MSPrintSchemaKeywordMap**定義では、プリントスキーマ機能キーワードへの ppd 機能キーワードのマッピングは、(format 1 を使用して) ppd 機能の前の \***MSPrintSchemaKeywordMap**定義で定義されているものと同じである必要があります。

-   PPD オプションキーワードは、以前の PPD ファイルコンテンツで既に定義されている PPD 機能のオプションを参照する必要があります。

-   PPD 機能の同じ PPD オプションに対する \***MSPrintSchemaKeywordMap**の複数の定義は許可されていません。 複数の定義が見つかった場合は、最初の定義のみが受け入れられ、他の定義は無視されます。

\***MSPrintSchemaKeywordMap**エントリが上記のいずれかの書式規則に違反している場合、そのエントリは無視され、詳細情報を含む ppdchecker 警告が表示されます。

**重要**   \*MSPrintSchemaKeywordMap は、次の標準の PPD 機能では使用できません。

\*\*双方向 \*InputSlot \*OutputBin \*PageSize \*Resolution \*MediaType、PPD ファイルで既に使用されている Print Schema キーワードに機能をマップすると、対応する PrintCapabilities ドキュメントによってその機能が複数回表示されることを理解しておくことが重要です。 複数のオカレンスがあると混乱する可能性があるため、PPD ファイルで使用される印刷スキーマキーワードに機能をマップしないでください。

 

  、PPD パーサーによって InputBin 機能の FORMSOURCE オプションが自動的に生成され、印刷スキーマの自動選択キーワードにマップされる**ことに注意**してください。 **MSPrintSchemaKeywordMap**属性を使用してオプションを print schema キーワードにマップする inputbin オプションが PPD ファイルに含まれている場合、印刷スキーマの機能には、デバイスの名前空間の formsource オプションが含まれます。 自動選択は PrintCapabilities ドキュメントに表示され、PPD ファイルの**MSPrintSchemaKeywordMap**属性に指定されているオプションを参照します。

 

次のコード例は、部分的な PPD ファイルの**MSPrintSchemaKeywordMap**属性の例を示しています。

```cpp
*OpenUI *IHVStapling:PickOne
*DefaultIHVStapling:Disabled
*IHVStapling Enabled:"..."
*IHVStapling Disabled:"..."
*CloseUI: *IHVStapling

*MSPrintSchemaKeywordMap: Staple*IHVStapling
*MSPrintSchemaKeywordMap: StapleOn*IHVStaplingEnabled
*MSPrintSchemaKeywordMap: StapleOff*IHVStaplingDisabled
```

### <a name="msprintschemaprivatenamespaceuri"></a>MSPrintSchemaPrivateNamespaceURI

**MsPrintSchemaPrivateNamespaceURI**属性は、コアドライバーが PrintTicket または PrintCapabilities のプライベートな PPD 機能またはオプションを公開するために使用するプライベート名前空間 URI を定義します。 この URI は、(\***MSPrintSchemaKeywordMap**定義を使用した) 明示的なマッピングを持たないすべての機能またはオプションに、パブリック印刷スキーマに適用されます。

**MSPrintSchemaPrivateNamespaceURI**は、次の形式を使用します。

```cpp
*MSPPrintSchemaPrivateNamespaceURI: "<URI>"
```

&lt;URI&gt; は、PPD QuotedValue を表します。 QuotedValue は、PPD 仕様で定義されているように、リテラル ASCII 部分文字列と16進部分文字列の両方を許可します。

1つのプリンターモデルの PPD ファイル (またはファイル) には \***MSPrintSchemaPrivateNamespaceURI**の定義が1つだけ必要です。 複数の定義が見つかった場合は、最初の定義のみが受け入れられ、他の定義は無視されます。

次のコード例は、部分的な PPD ファイルの**MsPrintSchemaPrivateNamespaceURI**属性の例を示しています。

```cpp
*MSPrivateNamespaceURI:  "https://www.ihv.com/schema/2004"
```

### <a name="msisxpsdriver"></a>MSIsXPSDriver

**MSIsXPSDriver**属性では、次の形式を使用します。

```cpp
*MSIsXPSDriver:  True | False
```

Windows Vista PScript5 driver configuration モジュール (Ps5ui) は、Microsoft Win32 GDI ドライバーと[新しい XPSDrv ドライバー](xpsdrv-printer-drivers.md)の両方に使用できます。 XPSDrv ドライバーの PScript5 driver 構成モジュールを使用するには、XPSDrv ドライバーの PPD データファイルで**MSIsXPSDriver**を指定し、その値を True に設定する必要があります。

次のコード例は、部分的な PPD ファイルでのこの属性の例を示しています。

```cpp
*MSIsXPSDriver: True
```

Win32 GDI ドライバー用の PScript5 driver 構成モジュールを使用するには、この PPD 属性を指定する必要はありません。

### <a name="msprintprocduplexoptions"></a>MSPrintProcDuplexOptions

**MSPrintProcDuplexOptions**属性では、次の形式を使用します。

```cpp
*MSPrintProcDuplexOptions:  "int"
```

この属性には、次のいずれかの値を指定できます。

1: リバース両面のページを反転する

2: 可能な場合は、余分な空白ページの生成を抑制します。

3: 上記の両方

0: 上記のいずれにも該当しません。

次のコード例は、部分的な PPD ファイル内の**MSPrintProcDuplexOptions**の例を示しています。

```cpp
*MSPrintProcDuplexOptions:  "2" 
```

この属性は、プリントプロセッサのさまざまな二重オプションを制御します。

**MSPrintProcDuplexOptions**が1の場合、印刷プロセッサが逆方向の両面でページを反転するかどうかを制御します。

4ページのドキュメントを n アップ = 1 で印刷する必要があり、逆印刷と両面印刷を使用する場合を想定しています。 印刷を反転させるには、最初のページの前にある最後のページを印刷します。 両面印刷が必要なので、1枚の用紙に2ページを印刷することをお勧めします。 印刷プロセッサは、次の2つの形式のいずれかでページを再生できます (各数値のペアは、1枚の用紙の両面に印刷される2ページを示します)。

-   形式 1: (4, 3)、(2, 1)

-   形式 2: (3, 4)、(1, 2)

Windows Vista より前の印刷プロセッサでは、2 \[(3, 4)、(1, 2)\]の形式でページが印刷されます。 ただし、Windows Vista 以降では、既定の形式は 1 \[(4, 3)、(2, 1)\]です。 この変更は、多くのプリンターの出力の形式が2で正しくないために発生しました。つまり、印刷されるページの順序は適切ではありません。

プリンターが形式1で正しく動作する場合、Windows Vista 以降では何も変更する必要はありません。 ただし、プリンターが形式1で正しく動作しない場合に、フォーマット2に戻すには、 **MSPrintProcDuplexOptions**属性を値1で追加します。

```cpp
*MSPrintProcDuplexOptions: "1"
```

Windows vista より前の PScript ドライバーでは、Windows Vista より前の印刷プロセッサを使用している場合、形式2が既定値であるため、動作を変更することはできません。それ以外の場合は、Windows Vista のプリントプロセッサがある場合、format 1 が既定値であるため、動作を変更することはできません。

Windows Vista PScript ドライバーの場合。 Windows Vista より前の印刷プロセッサを使用している場合、format 2 が既定値で、PPD 属性は無視されます。それ以外の場合、Windows Vista のプリントプロセッサがある場合は、フォーマット1が既定ですが、 **MSPrintProcDuplexOptions**属性を使用して形式を変更できます。

**MSPrintProcDuplexOptions**が2の場合、プリントプロセッサは、特定の二重シナリオで空白ページの生成を抑制します。

たとえば、ジョブが1ページのジョブで、両面がオン (n アップ = 1) である場合、用紙の片面だけを印刷する必要があります。 現時点では、プリンターは片面に印刷し、空の空のページを反転させることができます。 (印刷ジョブは双方向 = on で開始されているため、プリンターはシートを取り出す前に2ページが必要です。 2番目のページが印刷されない場合、一部のプリンタは待機状態を維持します。)現在のソリューションの欠点は次のとおりです。

-   生成されたページにより、アカウンティングソフトウェアのページ数とプリンター内のページカウンターが不正確になります。

-   プリンターの途中でページが印刷されると (一部の Hewlett-packard DeskJet スタイルのプリンター)、プリンターがそのページをプルしようとしている間に、ユーザーがそのページを取り出しようとすることがあります。 このような状況では、ハードウェアの問題が発生する可能性があります。

この問題を回避するには、PPD ファイルで \***MSPrintProcDuplexOptions**: "2" を指定します。

この属性が設定されている場合でも、空白のページの最適化は、次の限られた場合にのみ実行されることに注意してください。

1.  リバース印刷の場合、空白のページの最適化は、ジョブ全体が1つの用紙に収めることができる場合にのみ実行されます (たとえば、n アップ = 1 の aone ページジョブや、n アップ = 4 の4ページのジョブ)。 ジョブに複数のシートが必要な場合、最適化は実行されません (プリンターページが正しくない順序で印刷されるため)。 たとえば、3ページのジョブの場合、ページは注文3、2、1の順に印刷されます。4、3、2、&lt;空白の&gt;ではなく、空白&gt;&lt;ます。

2.  印刷プロセッサでコピーをシミュレートする必要がある場合、空白のページの最適化は performedd ません。 印刷プロセッサでは、必要なコピーの数がプリントプロセッサが実現できるコピーの数を超えている場合、コピーがシミュレートされます。

    次の状況は、シミュレーションが発生し、空白のページが生成される場合の例です (必要な場合)。

    -   コピーを作成できないプリンターの2つのコピー

    シミュレーションが実行されず、余分なページの生成を抑制できる場合は、次の状況が examles ます。

    -   コピーを作成できないプリンターの単一コピージョブ
    -   複数のコピーを作成できるプリンターの5つのコピージョブ

Windows Vista より前の PScript ドライバーでは、Windows Vista より前の印刷プロセッサを使用している場合、プリンターは必要に応じて余分な空白ページを印刷し、動作を変更することはできません。Windows Vista のプリントプロセッサを使用している場合は、必要に応じて余分な空白のページが印刷され、動作を変更することはできません。

Windows Vista PScript ドライバーの場合。 Windows Vista より前のプリントプロセッサを使用している場合は、必要に応じて余分な空白のページが印刷され、PPD 属性は無視されます。それ以外の場合、Windows Vista の印刷プロセッサを使用していて、適切な PPD 属性と適切な条件が存在する場合 (つまり、前に説明した空白ページの印刷を禁止する条件)、プリンターは空白のページを印刷しません。

### <a name="msbidiqueryfile"></a>MSBidiQueryFile

**Msbidiqueryfile**属性では、次の形式を使用します。

```cpp
*MSBidiQueryFile: "filename"
```

**Msbidiqueryfile**を使用して、プリンタドライバの自動 Config BidiQuery と BidiResponse データを含む GPD ファイル名または gdl ファイル名を指定します。 GPD または GDL ファイル名にパスを指定することはできません。

次のコード例は、部分的な PPD ファイル内の**Msbidiqueryfile**の例を示しています。

```cpp
*MSBidiQueryFile: "ACnfgPS.GDL"
```

### <a name="msxpsmaxcopies"></a>MSXPSMaxCopies

**MSXPSMaxCopies**属性では、次の形式を使用します。

```cpp
*MSXPSMaxCopies: "int"
```

**MSXPSMaxCopies**を使用して、XPSDrv プリンタードライバーがサポートできるコピーの最大数を指定します。

次のコード例は、部分的な PPD ファイル内の**MSXPSMaxCopies**の例を示しています。

```cpp
*MSXPSMaxCopies: "99"
```

 

 




