---
title: Windows Vista の新しいルート レベル専用 GPD 属性
description: Windows Vista の新しいルート レベル専用 GPD 属性
ms.assetid: 09f38459-6062-4d2a-9aee-929aa60193cf
keywords:
- ルート レベルのみ属性 WDK Unidrv
- 一般的なプリンター WDK Unidrv、ルート レベルのみの属性します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 396b844eecb6d4747d200856fa63ee0833bdac73
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578096"
---
# <a name="new-root-level-only-gpd-attributes-for-windows-vista"></a>Windows Vista の新しいルート レベル専用 GPD 属性


次の一覧には、Windows Vista と共に登場した新しい GPD 属性について説明します。 旧バージョンと Windows の以前の Windows Vista バージョンとの互換性を維持するには、これらの属性を次のコードを囲む必要があります。

```cpp
*Ifdef: WINNT_60 ... *Endif: WINNT_60 blocks
```

### <a name="printprocduplexoptions"></a>PrintProcDuplexOptions

**PrintProcDuplexOptions**属性は、プリント プロセッサのさまざまな二重化オプションを制御します。 この属性は、次の値の 1 つがあります。

1:反転双方向の反転のページ

2:可能であれば、余分な空白ページの生成を抑制します。

3:上記の両方

0:上記以外

場合**PrintProcDuplexOptions** 1 では、プリント プロセッサが反転双方向のページを回転する必要があるかどうかを制御します。

N を 4 ページの文書を印刷できると想定 = 1、逆の印刷や両面印刷を使用するとします。 最初のページの前に最後のページを印刷する逆の印刷をするためです。 両面印刷をするため、1 枚の用紙に 2 つのページを印刷します。 プリント プロセッサを再生できますページ (数字の各ペアは 1 枚の用紙の両面印刷は 2 つのページを示します) 次の 2 つの形式のいずれかで。

-   形式 1:(4,3),(2,1)

-   形式 2:(3,4),(1,2)

Windows Vista では、前に、プリント プロセッサが 2 の形式で注文を印刷は\[(3,4),(1,2)\]します。 Windows Vista 以降では、既定の形式には 1 の形式が\[(4,3),(2,1)\]します。 多くのプリンターがある 2; の形式で出力が正しくないために、この変更が発生しましたつまり、印刷されるページでは、適切な順序で順序がありません。

1 の形式で、プリンターが正常に動作する場合、Windows Vista 以降のものを変更する必要はありません。 ただし、プリンターが 1 の形式でなく正しく機能 2 の形式に戻したい場合は、GPD ファイルに次のコード例を追加します。

```cpp
*Ifdef: WINNT_60
*PrintProcDuplexOptions: 1
*Endif: WINNT_60
```

形式 1 は、いくつかの方向でよりよく動作可能性があります。 または入力と出力トレイ、および 2 形式の組み合わせは、その他の組み合わせでよりよく動作可能性があります。 その結果、配置することができます、 **PrintProcDuplexOptions**スイッチ/ケースのコンス トラクターの属性。

以前の Windows Vista Unidrv ドライバーでは、プリント プロセッサの以前の Windows Vista の場合は、形式 2 は、既定で、形式を変更することはできません。それ以外の場合、Windows Vista がプリント プロセッサがあれば、1 形式は、既定値と形式を変更することはできません。

Windows Vista Unidrv ドライバーの場合、以前の Windows Vista のプリント プロセッサがあれば、形式 2 は、既定で GPD 属性は無視されます。それ以外の場合、1 の形式は、既定ではを使用して形式を変更することができますが、Windows Vista のプリント プロセッサにある場合、 **PrintProcDuplexOptions**属性。

場合**PrintProcDuplexOptions**が 2 の場合、特定の双方向シナリオでの空白のページの生成を防ぐことができます。

この属性は、かどうかが送信する余分な空白ページをプリンターに両面印刷を実行している場合を制御します。 たとえば、ジョブが 1 ページの場合ジョブと双方向が (n を前提としています = 1)、シートの 1 つだけの側を印刷する必要があります。 現時点では、プリンターは一方の側を印刷して、裏面に空の空白ページを生成します。 (双方向で印刷ジョブが開始されたため、=、プリンターでは、シートを外れる前に、2 つのページが必要です。 2 番目のページが印刷されない場合は、一部のプリンター待機しています。)現在のソリューションの欠点は、です。

-   生成されたページは、会計ソフトウェア、プリンターでページ カウンター内の不正確なページ数です。

-   ページ (一部の Hewlett Packard DeskJet スタイル プリンター) で、プリンターから中間場合は、ユーザーがでそれを取得するプリンターの試行がバックアップ中に引き出しますしようとします。 このような状況には、ハードウェアの問題が発生します。

指定することで、上記の問題を回避できます\* **PrintProcDuplexOptions**:GPD ファイルに 2 です。

場合でも、この属性を設定するに、空白のページの最適化が次の制限付きの場合にのみ実行されることに注意してください。

1.  用紙の片面全体のジョブに収まる場合にのみ、逆の印刷時に空白のページの最適化が実行される (n を 1 ページ ジョブなど = 1 または n を 4 ページ ジョブ = 4)。 ジョブは、複数のシートを必要とする場合 (プリンター ページは、不正確な順序で印刷する) ため、最適化は実行されません。 たとえば、3 ページ ジョブが印刷するページ 3,2,1、順番&lt;空白&gt;4,3,2 ではなく&lt;空白&gt;します。

2.  コピーをシミュレートするために、プリント プロセッサがある場合は、空白のページの最適化は実行されません。 プリント プロセッサは、必要なコピーの数が、プリント プロセッサが、コピーの数を超える場合、コピーをシミュレートします。

    次のような状況は、シミュレーションが発生し、空のページが生成されます (必要な) 場合の例を示します。

    -   コピーを作成することはできませんのプリンターの 2 つのコピー

    次の状況は、examles シミュレーションが存在しないと、余分なページの生成を抑制することができます。

    -   コピーを作成することはできませんのプリンターの 1 つのコピー ジョブ
    -   5 つコピー ジョブにプリンターが可能な 1 つ以上にコピーします。

**PrintProcDuplexOptions の使用状況**

```cpp
*Ifdef: WINNT_60
*PrintProcDuplexOptions: 2
*Endif: WINNT_60 
```

場合によっては、それ以外の場合の実行時に余分なページが印刷しない念可能性があります。 そのため、配置することができます、 **PrintProcDuplexOptions**スイッチ/ケースのコンス トラクターの属性。

以前の Windows Vista Unidrv ドライバー、以前の Windows Vista のプリント プロセッサがある場合は、プリンター、必要と判断した場合、余分な空白ページが印刷されます。 この動作を変更することはできません。それ以外の場合、Windows Vista のプリント プロセッサがある場合は、プリンター、必要と判断した場合、余分な空白ページが印刷され、この動作を変更することはできません。

Windows Vista Unidrv ドライバー、Windows Vista のプリント プロセッサがある場合は、プリンター、必要と判断した場合、余分な空白ページが印刷されます GPD 属性は無視されます。それ以外の場合、Windows Vista のプリント プロセッサがある場合、適切な GPD 属性と、適切な条件がある場合 (つまり、防止について前に説明する条件を空のページ印刷)、プリンターは空白のページを印刷されません。

### <a name="preanalysisoptions"></a>PreAnalysisOptions

**PreAnalysisOptions**属性には、次の値のいずれかができます。

0:すべての事前分析モードを無効にします。

1:既定モードです。 モノクロの z オーダーのテキストの分析と空白のバンドの最適化を有効にします。 ダウンロード可能なフォントまたはデバイス フォントのサポートと高解像度を使用したデバイスのこのモードが有効になっている (600 dpi 以上)、24 bpp レンダリング モード。

2:24 ビット/ピクセル イメージ処理のコールバック関数の 1 ビット/ピクセルの最適化を有効にします。

4:デバイスの StretchBlt サポートを有効にします。

8:ベンダーの事前分析モードを有効にします。

16:24 ビット/ピクセルに、イメージ処理のコールバック関数を呼び出す前に、band が変換された 1 のビット/ピクセルのデバッグ モードを有効にします。

### <a name="usebmpfontcompression"></a>UseBMPFontCompression でしょうか。

**UseBMPFontCompression?** 属性では、フォントをビットマップとしてダウンロードするときに、Unidrv がデータを圧縮するかどうかを制御します。 既定値**UseBMPFontCompression?** は**FALSE**、つまり、この属性が GPD ファイル内に存在しない場合は、Unidrv に圧縮は実行されません。 この既定値は、ビットマップのフォントの圧縮機能がない Unidrv の以前のバージョンとの互換性を維持します。 この属性を設定する必要があります**TRUE**プリンターは、ビットマップ フォント圧縮あっしゅくビットマップ文字データをサポートしている場合にのみが圧縮された実行の長さで行繰り返し形式。

### <a name="usemode5compression"></a>UseMode5Compression でしょうか。

**UseMode5Compression?** 属性 UniDrv モード 5 圧縮を使用する必要があるかどうかを制御します。 5 モード (またはメソッドの 5) の圧縮はアダプティブ圧縮の他の複数の圧縮方法 (Unencoded、TIFF、デルタ行など) の組み合わせを使用できるようにします。 既定値**UseMode5Compression?** は**FALSE**、つまり、この属性が、GPD に存在しない場合は、Unidrv にアダプティブ圧縮は実行されません。 この既定値は、アダプティブ圧縮機能がない Unidrv の以前のバージョンとの互換性を維持します。 この属性を設定する必要があります**TRUE**プリンターには、アダプティブ圧縮がサポートされている場合にのみです。

### <a name="usehpglpolylineencoding"></a>UseHPGLPolylineEncoding でしょうか。

**UseHPGLPolylineEncoding?** 属性 Unidrv がポリラインのエンコーディングを使用する必要があるかどうかを制御します。 HP-GL/2 のペンをサポートしています]、[ペンのダウン/ベクトルを描画するための相対的な絶対/描画の描画コマンドします。 ポリライン エンコード (PE) のコマンドは、ベクトルを表すのより効率的な方法です。

既定値**UseHPGLPolylineEncoding?** は**FALSE**、つまり、この属性が GPD に存在しない場合は、Unidrv に PE コマンドは使用できません。 この既定値は、PE コマンドのサポートがない Unidrv の以前のバージョンとの互換性を維持します。 この値を設定する必要があります**TRUE**プリンターには、エンコードされたポリラインがサポートしている場合のみです。

### <a name="printschemaprivatenamespaceuri"></a>PrintSchemaPrivateNamespaceURI

**PrintSchemaPrivateNamespaceURI**属性が名前空間がプライベート コア ドライバーがプライベート PPD 機能またはオプションか、PrintTicket と PrintCapabilities で公開するために使用する URI を定義します。 この属性は、GPD ドキュメントのルートに表示する必要があり、ASCII 表示 PrintTickets と PrintCapabilities ドキュメント内の名前空間の定義に使用される URI にはが含まれています。 URI、さらに、関連付けられるすべての機能とパブリックのスキーマに明示的なマッピングがないこと、またはコアのドライバーが認識されないオプション。

### <a name="printschemakeywordmap"></a>PrintSchemaKeywordMap

**PrintSchemaKeywordMap**属性は、機能とオプションが表示されます、GPD ファイルを構築します。 この属性は、プリンター定義機能を使用する必要がどのようなパブリック印刷スキーマ名を示します。 二重を使用して PrintTicket の部単位で印刷する場合を除き、GPD ファイルで指定されている任意のオプションの名前を変更することができます、 **PrintSchemaKeywordMap**属性。

**注**   GPD パーサーが明示的に認識、ページ サイズ、色などの機能には、この属性は無視されます。

 

すべての値は、引用符で囲む必要があります。 これらは、存在する場合に、GPD で指定されているコード ページを使用して Unicode に変換されます。 その他の GPD 属性と同じ方法ですべての属性の定義が重複を解決します。読み取られる最後の定義には、優先順位が与えられます。

**重要な**  対応する PrintCapabilities ドキュメントがその機能を複数回一覧可能性があります GPD ファイルで既に使用されている印刷スキーマ キーワードに機能をマップした場合。 複数回出現は、機能、GPD ファイルで使用される印刷スキーマのキーワードをマップする必要がありますので、混乱を招く可能性があります。

 

**注**  GPD パーサーは自動的に InputBin 機能 FORMSOURCE オプションを生成し、印刷スキーマで、自動選択はキーワードにマップします。 GPD ファイルには使用する InputBin オプションが含まれて かどうか、 **PrintSchemaKeywordMap**印刷スキーマ キーワード オプションにマップする属性、印刷スキーマの機能がデバイスの名前空間で FORMSOURCE オプションが含まれます。 自動選択は PrintCapabilities ドキュメントに表示され、オプションで指定されているを参照してください、 **PrintSchemaKeywordMap** GPD ファイルの属性です。

 

次のコード例では、レイアウトを表示する部分 GPD ファイルを示します。

```cpp
*Feature: HPSTAPLER
{
    *Name: "Staple"
    *DefaultOption: Off
    * PrintSchemaKeywordMap: "Staple"

    *Option: Off
    {
        *Name: "Off"
        * PrintSchemaKeywordMap: "Off"
    }
 
    *Option: On
    {
        *Name: "On"
        * PrintSchemaKeywordMap: "On"
    }
}
```

### <a name="isxpsdriver"></a>IsXPSDriver

**IsXPSDriver**属性は次の GPD 構文を使用します。

```cpp
*IsXPSDriver?: TRUE | FALSE
```

Windows Vista Unidrv 構成モジュール (Unidrvui.dll) を使用するには Microsoft Win32 GDI ドライバーと、新しい[XPSDrv ドライバー](xpsdrv-printer-drivers.md)します。 XPSDrv ドライバー Unidrv 構成モジュールを使用する、XPSDrv ドライバーの GPD データ ファイルを指定する必要があります、 **IsXPSDriver**属性し、その値に設定**TRUE**します。

たとえば、XPS ドライバーがある場合は、次のコードを使用します。

```cpp
*IsXPSDriver?: TRUE
```

Win32 GDI ドライバー Unidrv 構成モジュールを使用するには、この属性を指定する必要はありません。

### <a name="useimageforhatchbrush"></a>UseImageForHatchBrush でしょうか。

**UseImageForHatchBrush?** 属性は次の GPD 構文を使用します。

```cpp
*Ifdef: WINNT_60
*UseImageForHatchBrush?: TRUE
*Endif: WINNT_60 
```

Microsoft Windows Server 2003 または Windows XP、ハッチ ブラシがで受信した場合に、Unidrv が HP-GL/2 のモードで印刷するときに、 [ **DrvRealizeBrush** ](https://msdn.microsoft.com/library/windows/hardware/ff556273)関数、Unidrv コマンドを送信、プリンターを選択できるように、適切なハッチ ブラシ。 Unidrv は、ハッチ ブラシをレンダリングする方法を制御しません。 たとえば、します線の間隔は通常、解像度によって制御します。 以上の解像度より低い解像度の小規模、中に、間隔を取得、間隔が大きくなります。 そのため、ドキュメントは可能性があります別の解像度を使用する場合、異なる方法で印刷します。

GPD が指定されている場合、Windows Vista では、 **UseImageForHatchBrush でしょうか。** 属性、Unidrv はビットマップのサーフェイスにハッチ ブラシをレンダリングし、デバイスにそのビットマップを送信します。 したがって、Unidrv には、ハッチ ブラシをレンダリングする方法のいくつかのコントロールがあります。

### <a name="reversebandorder"></a>ReverseBandOrder でしょうか。

**ReverseBandOrder?** 属性は次の GPD 構文を使用します。

```cpp
*Ifdef: WINNT_60
*ReverseBandOrder?: TRUE
*Endif: WINNT_60 
```

値**ReverseBandOrder でしょうか。** は**TRUE**または**FALSE**をリバース縞模様が有効になっているかどうかを示します。 この属性は、バンドの逆の順序で行われるようにします。 たとえば、縦向きの縞模様に発生します下から上下からではなくページのトップへ。

この属性は、基本的には ReverseBandOrderForEvenPages と同じでしょうかただし、 **ReverseBandOrder でしょうか。** でもと見なされます双方向の場合がアクティブでない (**ReverseBandOrderForEvenPages でしょうか。** 場合にのみ、works。双方向が ON) のすべてのページの動作 (**ReverseBandOrderForEvenPages でしょうか。** は偶数ページに対してのみ機能)。 使用する方法の詳細について**ReverseBandOrder でしょうか。** およびその他の関連の情報を参照してください\* **ReverseBandOrderForEvenPages?** します。 特に、スキャン ラインと、スキャン ライン内のビットのプラグインが取り消す必要がありますに注意してください。

組み合わせを使用する\*ReverseBandOrderForEvenPages? と\* **ReverseBandOrder でしょうか。** します。

のみ**ReverseBandOrder?** に設定されている**TRUE**、すべてのページの縞模様は取り消されます。

のみ**ReverseBandOrderForEvenPages でしょうか。** に設定されている**TRUE**、縞模様元に戻されますでも pagesonly のプリンターが両面印刷を印刷します。 双方向が設定されていない場合、 **ReverseBandOrderForEvenPages?** 設定は無視されます。

ときに両方**ReverseBandOrder でしょうか。** と**ReverseBandOrderForEvenPages?** が設定すると、次のように。

-   場合双方向が ON に奇数ページ リバース縞模様が実行される (つまり、1、3、5、7、およびなど)。

-   場合 OFF は、双方向ですべてのページが実行されるリバース縞模様します。

### <a name="bidiqueryfile"></a>BidiQueryFile

**BidiQueryFile**属性は次の GPD 構文を使用します。

```cpp
*BidiQueryFile: <GPD or GDL file name>
```

使用**BidiQueryFile**プリンター ドライバーの自動構成を含む GPD または GDL ファイル名を指定する**BidiQuery**または**BidiResponse**データ。 GPD または GDL ファイル名は、任意のパスを指定しないでください。 値としてその GPD ファイルを指定できますも自動構成データが、ドライバーの DataFile GPD ファイル内で含まれている場合、 **BidiQueryFile**属性。

次のコード例では、部分的な GPD ファイルでこの属性の例を示します。

```cpp
*Ifdef: WINNT_60
*BidiQueryFile: "ACnfgUni.GDL"
*Endif: WINNT_60
```

 

 




