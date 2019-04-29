---
title: Windows Vista の新しいルート レベル専用 PPD 属性
description: Windows Vista の新しいルート レベル専用 PPD 属性
ms.assetid: 49cdfb2f-e119-4960-9e79-67e1025b753f
keywords:
- ルート レベルのみ属性 WDK Unidrv
- 一般的なプリンター WDK Unidrv、ルート レベルのみの属性します。
- PPD は、WDK Unidrv を属性します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30235aae4772d555ad99a7109b534c2f6bb67721
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330126"
---
# <a name="new-root-level-only-ppd-attributes-for-windows-vista"></a>Windows Vista の新しいルート レベル専用 PPD 属性


次の一覧には、Windows Vista と共に登場した新しい PPD 属性について説明します。 旧バージョンと Windows の以前の Windows Vista バージョンとの互換性を維持するには、これらの属性を次のコードを囲む必要があります。

```cpp
*Ifdef: WINNT_60 ... *Endif: WINNT_60 blocks
```

### <a name="msprintschemakeywordmap"></a>MSPrintSchemaKeywordMap

**MSPrintSchemaKeywordMap** PPD 機能キーワードからパブリックの印刷スキーマ機能キーワードへのマッピングを定義する属性または PPD の PPD オプション キーワードからのマッピング機能、印刷の public 印刷スキーマ オプションのキーワードスキーマの機能です。

**MSPrintSchemaKeywordMap**が使用可能な 2 つの形式。

<a href="" id="format-1"></a>形式 1  
```cpp
*MSPrintSchemaKeywordMap: PrintSchema_feature_keyword *<PPD_feature_keyword>
```

<a href="" id="format-2"></a>形式 2  
```cpp
*MSPrintSchemaKeywordMap: PrintSchema_feature_keyword PrintSchema_option_keyword *<PPD_feature_keyword> <PPD_option_keyword>
```

PPD 機能キーワードのプレフィックス (これは、アスタリスク\[ \* \]) 両方の形式が必要です。

形式 1。

-   PPD 機能のキーワードは、以前 PPD ファイルの内容で既に定義されている PPD 機能を参照する必要があります。

-   複数の定義\* **MSPrintSchemaKeywordMap**同じ PPD 機能は使用できません。 複数の定義が見つかった場合は、最初の定義のみが受け入れられますと他の定義は無視されます。

形式 2。

-   \* **MSPrintSchemaKeywordMap** (形式を使用して 1) PPD 機能の定義は、いずれかの前に存在する必要があります\* **MSPrintSchemaKeywordMap** PPD の定義機能のオプションを表示できます。

-   \* **MSPrintSchemaKeywordMap** PPD オプションの定義、PPD 機能キーワード印刷スキーマ機能のキーワードをマッピングする必要があります、以前に定義されているものと同じ\* **MSPrintSchemaKeywordMap** (形式を使用して 1) PPD 機能を定義します。

-   PPD オプションのキーワードは、以前 PPD ファイルの内容で既に定義されている PPD 機能のオプションを参照する必要があります。

-   複数の定義\* **MSPrintSchemaKeywordMap** PPD 機能のオプション同じ PPD 用にこの変更は許可されません。 複数の定義が見つかった場合は、最初の定義のみが受け入れられますと他の定義は無視されます。

場合、 \* **MSPrintSchemaKeywordMap**エントリの前の書式規則に違反、エントリが無視されますが、詳細な情報を ppdchecker 警告が表示されます。

**重要な**   \*MSPrintSchemaKeywordMap は、次の標準 PPD 機能で使用するためにサポートされていません。

\*Collate\*双方向\*InputSlot \*OutputBin \*PageSize\*解決\*MediaType It が既にある印刷スキーマ キーワードに機能をマップした場合を知っておく必要もPPD ファイルで使用されている、対応する PrintCapabilities ドキュメント一覧可能性があります機能は複数回です。 複数回出現は、機能を PPD ファイルで使用される印刷スキーマのキーワードをマップする必要がありますので、混乱を招く可能性があります。

 

**注**  PPD パーサーは自動的に InputBin 機能 FORMSOURCE オプションを生成し、印刷スキーマで、自動選択はキーワードにマップします。 PPD ファイルには使用する InputBin オプションが含まれて かどうか、 **MSPrintSchemaKeywordMap**印刷スキーマ キーワード オプションにマップする属性、印刷スキーマの機能がデバイスの名前空間で FORMSOURCE オプションが含まれます。 自動選択は PrintCapabilities ドキュメントに表示され、オプションで指定されているを参照してください、 **MSPrintSchemaKeywordMap** PPD ファイルの属性です。

 

コード例を次の例を示しています、 **MSPrintSchemaKeywordMap**部分 PPD ファイル内の属性。

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

**MsPrintSchemaPrivateNamespaceURI**属性が名前空間がプライベート コア ドライバーがプライベート PPD 機能またはオプションか、PrintTicket と PrintCapabilities で公開するために使用する URI を定義します。 この URI は、機能または明示的なマッピングがないオプションに適用されます (を使用して、 \* **MSPrintSchemaKeywordMap**定義) 印刷スキーマをパブリックにします。

**MSPrintSchemaPrivateNamespaceURI**は次の形式を使用します。

```cpp
*MSPPrintSchemaPrivateNamespaceURI: "<URI>"
```

&lt;URI&gt; PPD QuotedValue を表します。 PPD 仕様で定義されている、リテラルの ASCII 部分文字列と 16 進数の部分文字列の両方 QuotedValue ことができます。

1 つのプリンター モデルの PPD ファイル (またはファイル) が 1 つだけ定義の\* **MSPrintSchemaPrivateNamespaceURI**します。 複数の定義が見つかった場合は、最初の定義のみが受け入れられますがされ、他のユーザーは無視されます。

コード例を次の例を示しています、 **MsPrintSchemaPrivateNamespaceURI**部分 PPD ファイル内の属性。

```cpp
*MSPrivateNamespaceURI:  "http://www.ihv.com/schema/2004"
```

### <a name="msisxpsdriver"></a>MSIsXPSDriver

**MSIsXPSDriver**属性は、次の形式を使用します。

```cpp
*MSIsXPSDriver:  True | False
```

両方の Microsoft Win32 GDI ドライバーを Windows Vista PScript5 ドライバー構成モジュール (Ps5ui.dll) を使用して、[新しい XPSDrv ドライバー](xpsdrv-printer-drivers.md)します。 XPSDrv ドライバー PScript5 ドライバーの構成モジュールを使用する、XPSDrv ドライバーの PPD データ ファイルを指定する必要があります**MSIsXPSDriver**その値を True に設定します。

次のコード例では、部分的な PPD ファイルでこの属性の例を示します。

```cpp
*MSIsXPSDriver: True
```

Win32 GDI ドライバー PScript5 ドライバーの構成モジュールを使用するには、この PPD 属性を指定する必要はありません。

### <a name="msprintprocduplexoptions"></a>MSPrintProcDuplexOptions

**MSPrintProcDuplexOptions**属性は、次の形式を使用します。

```cpp
*MSPrintProcDuplexOptions:  "int"
```

この属性は、次の値の 1 つがあります。

1:反転双方向の反転のページ

2:可能であれば、余分な空白ページの生成を抑制します。

3:上記の両方

0:上記以外

コード例を次の例を示します**MSPrintProcDuplexOptions** PPD ファイルの一部分にします。

```cpp
*MSPrintProcDuplexOptions:  "2" 
```

この属性は、プリント プロセッサのさまざまな二重化オプションを制御します。

場合**MSPrintProcDuplexOptions** 1 では、プリント プロセッサが反転双方向のページを回転する必要があるかどうかを制御します。

N を 4 ページの文書を印刷できると想定 = 1、逆の印刷や両面印刷を使用するとします。 最初のページの前に最後のページを印刷する逆の印刷をするためです。 両面印刷をするため、1 枚の用紙に 2 つのページを印刷します。 プリント プロセッサを再生できますページ (数字の各ペアは 1 枚の用紙の両面印刷は 2 つのページを示します) 次の 2 つの形式のいずれかで。

-   形式 1:(4,3),(2,1)

-   形式 2:(3,4),(1,2)

Windows Vista では、前に、プリント プロセッサが 2 の形式でページを印刷は\[(3,4),(1,2)\]します。 Windows Vista 以降では、既定の形式には 1 の形式が\[(4,3),(2,1)\]します。 多くのプリンターがある 2; の形式で出力が正しくないために、この変更が発生しましたつまり、印刷されるページでは、適切な順序で順序がありません。

プリンターが 1 の形式で正常に動作する場合は、Windows Vista 以降のものを変更する必要はありません。 ただし、2 という形式に戻すには、プリンターで 1 形式に正しく動作する場合は、追加、 **MSPrintProcDuplexOptions**値 1 を持つ属性です。

```cpp
*MSPrintProcDuplexOptions: "1"
```

以前の Windows Vista PScript ドライバーの場合、以前の Windows Vista のプリント プロセッサがあれば、形式 2 は、既定で; の動作を変更することはできません。それ以外の場合、Windows Vista がプリント プロセッサがあれば、1 の形式は、既定では、および動作を変更することはできません。

Windows Vista PScript ドライバー。 プリント プロセッサの以前の Windows Vista の場合は、2 の形式は、既定値と PPD 属性は無視されます。それ以外の場合、1 の形式は、既定ではを使用して形式を変更することができますが、Windows Vista のプリント プロセッサにある場合、 **MSPrintProcDuplexOptions**属性。

場合**MSPrintProcDuplexOptions**が 2 のプリント プロセッサが特定の双方向シナリオでの空白のページの生成を抑制します場合。

たとえば、上、ジョブがジョブの 1 ページ、双方向の場合は (n を前提としています = 1)、シートの 1 つだけの側を印刷する必要があります。 現時点では、プリンターは一方の側を印刷して、裏面に空の空白ページを生成します。 (双方向で印刷ジョブが開始されたため、=、プリンターでは、シートを外れる前に、2 つのページが必要です。 2 番目のページが印刷されない場合は、一部のプリンター待機しています。)現在のソリューションの欠点は次のとおりです。

-   生成されたページは、会計ソフトウェア、プリンターでページ カウンター内の不正確なページ数です。

-   ページ (一部の Hewlett Packard DeskJet スタイル プリンター) で、プリンターから中間場合は、ユーザーがでそれを取得するプリンターの試行がバックアップ中に引き出しますしようとします。 このような状況には、ハードウェアの問題が発生します。

指定することで、上記の問題を回避できます\* **MSPrintProcDuplexOptions**:「2」PPD ファイルにします。

場合でも、この属性を設定するに、空白のページの最適化が次の制限付きの場合にのみ実行されることに注意してください。

1.  用紙の片面全体のジョブに収まる場合にのみ、逆の印刷時に空白のページの最適化が実行される (n を aone ページ ジョブなど = 1 または n を 4 ページ ジョブ = 4)。 ジョブは、複数のシートを必要とする場合 (プリンター ページは、不正確な順序で印刷する) ため、最適化は実行されません。 たとえば、3 ページ ジョブが印刷するページ 3,2,1、順番&lt;空白&gt;4,3,2 ではなく&lt;空白&gt;します。

2.  コピーをシミュレートするために、プリント プロセッサがある場合、空白のページの最適化が performedd です。 プリント プロセッサは、必要なコピーの数が、プリント プロセッサが、コピーの数を超える場合、コピーをシミュレートします。

    次のような状況は、シミュレーションが発生し、空のページが生成されます (必要な) 場合の例を示します。

    -   コピーを作成することはできませんのプリンターの 2 つのコピー

    次の状況は、examles シミュレーションが存在しないと、余分なページの生成を抑制することができます。

    -   コピーを作成することはできませんのプリンターの 1 つのコピー ジョブ
    -   コピーではなく、プリンターの 5 つコピー ジョブ

以前の Windows Vista PScript ドライバーが表示され、以前の Windows Vista のプリント プロセッサがある場合は、プリンター、必要と判断した場合、余分な空白ページが印刷されます; 動作を変更することはできません。それ以外の場合、Windows Vista のプリント プロセッサがある場合は、プリンター、必要と判断した場合、余分な空白ページが印刷され、動作を変更することはできません。

Windows Vista PScript ドライバー。 以前の Windows Vista のプリント プロセッサがあれば、プリンター、必要と判断した場合、余分な空白ページが印刷され、PPD 属性は無視されます。それ以外の場合、Windows Vista のプリント プロセッサがある場合、適切な PPD 属性と、適切な条件がある場合 (つまり、防止について前に説明する条件を空のページ印刷)、プリンターは空白のページを印刷されません。

### <a name="msbidiqueryfile"></a>MSBidiQueryFile

**MSBiDiQueryFile**属性は、次の形式を使用します。

```cpp
*MSBidiQueryFile: "filename"
```

使用**MSBiDiQueryFile**データが含まれる、プリンター ドライバーの自動構成 BidiQuery BidiResponse GPD または GDL ファイルの名前を指定します。 GPD または GDL ファイル名は、任意のパスを指定しないでください。

コード例を次の例を示します**MSBiDiQueryFile** PPD ファイルの一部分にします。

```cpp
*MSBidiQueryFile: "ACnfgPS.GDL"
```

### <a name="msxpsmaxcopies"></a>MSXPSMaxCopies

**MSXPSMaxCopies**属性は、次の形式を使用します。

```cpp
*MSXPSMaxCopies: "int"
```

使用**MSXPSMaxCopies** XPSDrv プリンター ドライバーをサポートできるコピーの最大数を指定します。

コード例を次の例を示します**MSXPSMaxCopies** PPD ファイルの一部分にします。

```cpp
*MSXPSMaxCopies: "99"
```

 

 




