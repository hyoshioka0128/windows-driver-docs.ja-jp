---
title: サポートされている PrintTicket 機能
description: このセクションでは、標準 XPS フィルターでサポートされている PrintTicket の機能についての情報を提供します。
ms.assetid: 6D1AD770-D4BA-4BDC-886A-C5C36A09BB0E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3390095e14b175eb411bce8c4de07a490e727ed5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559178"
---
# <a name="supported-printticket-features"></a>サポートされている PrintTicket 機能


このセクションでは、標準 XPS フィルターでサポートされている PrintTicket の機能についての情報を提供します。

これらすべての機能には、生成される PDL コマンドを変更するため、XPS フィルター効果があります。 フィルターによって PDL コマンドを生成するかどうか自体、またはこれらが GPD/PPD デバイスによって指定されると、XPS フィルター PDL コマンドを変更する原因となるこれらの機能です。 印刷スキーマ (psk) のキーワード名前空間には、すべての要素 (機能、オプション、ScoredProperties、パラメーター)、次のセクションで参照されているを確認できます。

## <a name="pagemediasize"></a>PageMediaSize


この機能では、印刷出力に使用されるメディア用紙のサイズについて説明します。 各オプションは、名だけでなく、スコア付けされた 2 つのプロパティを含めることができます。MediaSizeWidth MediaSizeHeight. これらには、物理メディアのサイズについて説明します。 サポートされているオプションは、対応する GPD/PPD ファイル エントリと、オプションです。

PCL6/GPD の PrintTicket オプションが場合 CustomMediaSize、PageMediaSizeMediaSizeWith と PageMediaSizeMediaSizeHeight パラメーター使用されますメディアのサイズを取得します。

PostScript/PPD、PrintTicket オプションは PSCustomMediaSize PageMediaSizePSWith しいて PageMediaSizePSHeight パラメーターを使用すると、メディアのサイズを取得します。 選択したメディアの種類に対して生成された PCL6 は GPD PageSize 機能の値によって指定されます。 次に、GPD が使用する PageMediaSize オプションかが調べられる順序を示します。

1. PrintSchemaKeywordMap が指定されており、PageMediaSize オプションの名前属性と一致します。

2. 次[PageMediaSize の既定のマッピング](default-pagemediasize-mappings.md)使用されます。

3. PageSize オプションの name 属性は、GPD でオプションの名前と一致します。

レンダリング プロセス中に、フィルターで置換されます PhysPaperWidth に対して GPD コマンドで MediaSizeWidth ScoredProperty または PageMediaSizeMediaSizeWidth パラメーターで指定された用紙の幅。

フィルターも置き換えます PhysPaperLength に対して GPD コマンドで MediaSizeHeight ScoredProperty または PageMediaSizeMediaSizeHeight パラメーターで指定された用紙の長さ。

選択したメディアの種類に対して生成された PostScript は PPD PageSize 機能によって指定されます。 次の順序で PPD で使用するオプションが選択されます。

1. MSPrintSchemaKeywordMap が指定されており、PageMediaSize オプションの名前属性と一致します。

2. PageSize オプションの name 属性、PPD. でオプションの名前に一致します。

## <a name="pagemediatype"></a>PageMediaType


この機能では、コーティング、メディアのマテリアル、およびメディアの太さなど、デバイスで使用できるメディアのシートの特性について説明します。 サポートされているオプションは、対応する GPD/PPD エントリで。

選択したメディアの種類に対して生成された PCL6 は GPD MediaType 機能によって指定されます。 次の順序で使用する、GPD でオプションが選択されます。

1. PrintSchemaKeywordMap が指定されており、PageMediaType オプションの名前属性と一致します。

2. 次の既定のマッピングが使用されます。

| PageMediaType 値            | GPD/PPD ファイルのエントリ |
|--------------------------------|--------------------|
| PrintTicket PhotographicGlossy | GPD 光沢紙         |
| PrintTicket プレーン              | GPD 標準       |
| PrintTicket の透過性       | GPD 透過性   |

 

3. PageMediaType オプションの name 属性は、GPD でオプションの名前と一致します。

選択したメディアの種類に対して生成された PostScript は PPD MediaType 機能によって指定されます。 次の順序で PPD で使用するオプションが選択されます。

1. MSPrintSchemaKeywordMap が指定されており、PageMediaType オプションの名前属性と一致します。

2. PageMediaType オプションの name 属性、PPD. でオプションの名前に一致します。

## <a name="pagemediacolor"></a>PageMediaColor


この機能には、メディアのシートの色がについて説明します。 サポートされているオプションは、対応する GPD/PPD エントリで。

選択したメディアの色が GPD 機能で指定されたために生成される PCL6 を含む\*PrintSchemaKeywordMap:"PageMediaColor"。 次の順序で使用する、GPD でオプションが選択されます。

1. PrintSchemaKeywordMap が指定されており、PageMediaColor オプションの名前属性と一致します。

2. PageMediaColor オプションの name 属性は、GPD でオプションの名前と一致します。

選択したメディア色に対して生成された PostScript は PPD MediaColor 機能によって指定されます。 次の順序で PPD で使用するオプションが選択されます。
1. MSPrintSchemaKeywordMap が指定されており、PageMediaColor オプションの名前属性と一致します。

2. PageMediaColor オプションの name 属性、PPD. でオプションの名前に一致します。

## <a name="jobinputbin"></a>JobInputBin


この機能では、印刷デバイスにメディアを引き出す入力場所について説明します。 サポートされているオプションは、対応する GPD/PPD エントリを持つです。

選択した入力トレイ用に生成 PCL6 は GPD InputBin 機能によって指定されます。 次の順序で使用する、GPD でオプションが選択されます。

1. PrintSchemaKeywordMap が指定されており、JobInputBin オプションの名前属性と一致します。

2. 次の既定のマッピングが使用されます。

| JobInputBin 値      | GPD/PPD ファイルのエントリ                  |
|------------------------|-------------------------------------|
| PrintTicket カセット   | GPD AUTO、カセット、ENVFEED、ENVMANUAL |
| PrintTicket の自動選択 | GPD FORMSOURCE                      |
| PrintTicket 高       | GPD LARGECAPACITY、LARGEFMT、削減します。    |
| PrintTicket 手動     | GPD MANUAL,MIDDLE,SMALLFMT          |
| PrintTicket の供給    | GPD 供給、上限                   |

 

3. PageMediaType オプションの name 属性は、GPD でオプションの名前と一致します。

選択した入力トレイに対して生成された PostScript は PPD InputSlot 機能によって指定されます。 次の順序で PPD で使用するオプションが選択されます。
1. MSPrintSchemaKeywordMap が指定されており、JobInputBin オプションの名前属性と一致します。

2. JobInputBin オプションの name 属性、PPD. でオプションの名前に一致します。

## <a name="pageorientation"></a>PageOrientation


この機能では、コンテンツの座標空間からシートのメディアの座標空間に変換するときに使用する回転変換を示します。 縦、横、ReversePortrait、ReverseLandscape、サポートされていることもできます。

選択した方向に対して生成された PCL6 は GPD 方向付けによって指定されます。 次の順序で使用する、GPD でオプションが選択されます。

1. PrintSchemaKeywordMap が指定されており、PageOrientation オプションの名前属性と一致します。

2. 次の既定のマッピングが使用されます。

| PageOrientation 値        | GPD/PPD ファイルのエントリ   |
|------------------------------|----------------------|
| PrintTicket の縦向き         | GPD 縦向き         |
| PrintTicket のランドス ケープ        | GPD ランドス ケープ\_CC90  |
| PrintTicket ReverseLandscape | GPD ランドス ケープ\_CC270 |

 

3. PageOrientation オプションの name 属性は、GPD でオプションの名前と一致します。

選択した方向に対して生成された PostScript はフィルターによって決まります。
## <a name="pageoutputcolor"></a>印刷


この機能は、移行先のドキュメント ページの印刷出力の色に関する特性 (色、モノクロ) を制御します。 サポートされているオプションは、色、グレースケールやモノクロです。

選択した出力の色に対して生成された PCL6 は GPD 返さ機能によって指定されます。 次の順序で使用する、GPD でオプションが選択されます。

1. PrintSchemaKeywordMap が指定されており、印刷オプションの名前属性と一致します。

2. 印刷オプションの name 属性は、GPD でオプションの名前と一致します。

選択した出力の色に対して生成された PostScript はフィルターによって決まります。
## <a name="pageresolution"></a>PageResolution


この機能は、デバイスに出力を生成できます (1 インチあたりのドット数) で使用可能な解像度を定義します。 印刷スキーマがこの機能のオプションの任意の標準名を指定しません。ただし、オプションの名前に関係なく 2 つの ScoredProperties をサポートしています。ResolutionX、ResolutionY とします。 サポートされているオプションは、対応する GPD/PPD エントリで。

選択した解決用に生成 PCL6 GPD 解決の機能を指定します。 次の順序で使用する、GPD でオプションが選択されます。

1. PrintSchemaKeywordMap が指定されており、PageResolution オプションの名前属性と一致します。

2. PageResolution オプションの name 属性は、GPD でオプションの名前と一致します。

レンダリング中に、フィルターで置換されます GraphicsXRes と TextXRes に対して GPD コマンドで ResolutionX で指定された水平方向の解像度。
フィルターは置き換えることも GraphicsYRes と TextYRes に対して GPD コマンドで ResolutionY で指定された垂直方向の解像度でします。

選択した解決用に生成 PostScript は、PPD 解像度または JCLResolution 機能によって指定されます。 次の順序で PPD で使用するオプションが選択されます。

1. MSPrintSchemaKeywordMap が指定されており、PageResolution オプションの名前属性と一致します。

2. PageResolution オプションの name 属性、PPD. でオプションの名前に一致します。

## <a name="pageoutputquality"></a>PageOutputQuality


この機能は、ドキュメントのページの印刷品質を定義します。 サポートされるオプションは、対応する GPD/PPD エントリを持つです。

選択した品質の生成 PCL6 は PageOutputQuality の PrintSchemaKeywordMap 値を持つ GPD 機能によって指定されます。 次の順序で使用する、GPD でオプションが選択されます。

1. PrintSchemaKeywordMap が指定されており、PageOutputQuality オプションの名前属性と一致します。

2. PageOutputQuality オプションの name 属性は、GPD でオプションの名前と一致します。

選択した品質に対して生成された PostScript は PageOutputQuality MSPrintSchemaKeywordMap 値を持つ PPD 機能によって指定されます。 次の順序で PPD で使用するオプションが選択されます。
1. MSPrintSchemaKeywordMap が指定されており、PageOutputQuality オプションの名前属性と一致します。

2. PageOutputQuality オプションの name 属性、PPD. でオプションの名前に一致します。

## <a name="jobcopiesalldocuments"></a>JobCopiesAllDocuments


このパラメーターは、印刷ジョブ内のすべてのドキュメントを出力する回数を指定します。

選択されているコピー用に生成 PCL6 はフィルターによって決まります。 このパラメーターとの対話 JobCollateAllDocuments 機能を参照してください。

選択したコピーに対して生成された PostScript はフィルターによって決まります。 このパラメーターとの対話 JobCollateAllDocuments 機能を参照してください。

## <a name="documentcopiesallpages"></a>DocumentCopiesAllPages


このパラメーターは、印刷ジョブに関連付けられているドキュメントを出力 ページのコピーの数を指定します。

選択されているコピー用に生成 PCL6 はフィルターによって決まります。 このパラメーターとの対話示さ機能を参照してください。

選択したコピーに対して生成された PostScript はフィルターによって決まります。 このパラメーターとの対話示さ機能を参照してください。

## <a name="pagecopies"></a>PageCopies


このパラメーターは、出力するドキュメント内の個々 のソース ドキュメントのページのコピーの数を指定します。 コピーの数は、現在のページにのみ適用されるので、照合順序はありません。

選択されているコピー用に生成 PCL6 はフィルターによって決まります。

選択したコピーに対して生成された PostScript はフィルターによって決まります。

## <a name="documentcollate"></a>示さ


この機能は、印刷出力の印刷ジョブに関連付けられているドキュメントのページが表示される順序を指定します。 丁合い、丁合いなしサポートされていることもできます。

選択された照合順序に対して生成された PCL6 GPD 部単位印刷機能を指定します。 次の順序で使用する、GPD でオプションが選択されます。

1. PrintSchemaKeywordMap を指定して、示さオプションの名前属性と一致する場合。

2. 次の既定のマッピングが使用されます。

| 示さ値  | GPD/PPD ファイルのエントリ |
|------------------------|--------------------|
| PrintTicket 丁合いなし | オフ GPD            |
| PrintTicket の部単位で印刷   | GPD             |

 

3. 示さオプションの name 属性は、GPD でオプションの名前と一致します。

**注**  丁合いに設定されているときに示さし GPD Collate オプションは、コマンドを含む、デバイスが部単位でのコピーを生成できることと見なされます。 *XPS.PCL6*フィルターはのみ、ジョブの 1 つのコピーを生成し、GPD コマンドを使用して、部単位でのコピーを生成するデバイスに指示します。 フィルターに置き換えます NumOfCopies GPD コマンドで JobCopiesAllDocuments で指定されたコピーの数。

 

選択された照合順序に対して生成された PostScript は PPD 部単位印刷機能によって指定されます。 次の順序で PPD で使用するオプションが選択されます。
1. MSPrintSchemaKeywordMap を指定して、示さオプションの名前属性と一致する場合。

2. 次の既定のマッピングが使用されます。

| 示さ値  | GPD/PPD ファイルのエントリ |
|------------------------|--------------------|
| PrintTicket 丁合いなし | PPD False          |
| PrintTicket の部単位で印刷   | PPD True           |

 

3. 示さオプションの name 属性、PPD. でオプションの名前に一致します。

**注**  丁合いに設定されているときに示さ、PPD には、Collate 機能、または示さにマップされているキーワードである機能が含まれていて、デバイスが部単位でのコピーを生成できることと見なされます。 XPS.PS フィルターはのみ、ジョブの 1 つのコピーを生成し、PPD コマンドを使用して、部単位でのコピーを生成するデバイスに指示します。

 

## <a name="jobduplexalldocumentscontiguously"></a>JobDuplexAllDocumentsContiguously


この機能は、ドキュメントの境界を考慮せず、印刷ジョブの両面印刷を指定します。 両面印刷が指定されている場合、印刷ジョブのすべてのドキュメントのすべてのページは双方向ドキュメント間の空白のページを挿入せずに継続的に印刷します。 OneSided、TwoSidedShortEdge、および TwoSidedLongEdge サポートされていることもできます。

選択した双方向に対して生成された PCL6 GPD 双方向機能を指定します。 次の順序で使用する、GPD でオプションが選択されます。

1. PrintSchemaKeywordMap が指定されており、JobDuplexAllDocumentsContiguously オプションの名前属性と一致します。

2. 次の既定のマッピングが使用されます。

| JobDuplexAllDocumentsContiguously 値 | GPD/PPD ファイルのエントリ |
|-----------------------------------------|--------------------|
| PrintTicket OneSided                    | GPD なし           |
| PrintTicket TwoSidedShortEdge           | GPD 水平     |
| PrintTicket TwoSidedLongEdge            | GPD 垂直       |

 

3. JobDuplexAllDocumentsContiguously オプションの name 属性は、GPD でオプションの名前と一致します。

選択した双方向に対して生成された PostScript は PPD で使用するオプションが次の順序で選択されている PPD 双方向機能によって指定されます。
1. MSPrintSchemaKeywordMap が指定されており、JobDuplexAllDocumentsContiguously オプションの名前属性と一致します。

2. 次の既定のマッピングが使用されます。

| JobDuplexAllDocumentsContiguously 値 | GPD/PPD ファイルのエントリ |
|-----------------------------------------|--------------------|
| PrintTicket OneSided                    | PPD なし           |
| PrintTicket TwoSidedShortEdge           | PPD DuplexTumble   |
| PrintTicket TwoSidedLongEdge            | PPD DuplexNoTumble |

 

3. JobDuplexAllDocumentsContiguously オプションの name 属性、PPD. でオプションの名前に一致します。

## <a name="documentduplex"></a>DocumentDuplex


この機能は、印刷ジョブに関連付けられているドキュメントの両面印刷を制御します。 これが指定されている場合は、メディアの新しいシートの前面にある印刷出力が開始します。 サポートされているオプションは、OneSided、TwoSidedShortEdge、TwoSidedLongEdge です。

選択した双方向に対して生成された PCL6 GPD 双方向機能を指定します。 次の順序で使用する、GPD でオプションが選択されます。

1. PrintSchemaKeywordMap が指定されており、DocumentDuplex オプションの名前属性と一致します。

2. 次の既定のマッピングが使用されます。

| DocumentDuplex 値          | GPD/PPD ファイルのエントリ |
|-------------------------------|--------------------|
| PrintTicket OneSided          | GPD なし           |
| PrintTicket TwoSidedShortEdge | GPD 水平     |
| PrintTicket TwoSidedLongEdge  | GPD 垂直       |

 

3. DocumentDuplex オプションの name 属性は、GPD でオプションの名前と一致します。

選択した双方向に対して生成された PostScript は PPD 双方向機能によって指定されます。 次の順序で PPD で使用するオプションが選択されます。
1. MSPrintSchemaKeywordMap が指定されており、DocumentDuplex オプションの名前属性と一致します。

2. 次の既定のマッピングが使用されます。

| DocumentDuplex 値          | GPD/PPD ファイルのエントリ |
|-------------------------------|--------------------|
| PrintTicket OneSided          | PPD なし           |
| PrintTicket TwoSidedShortEdge | PPD DuplexTumble   |
| PrintTicket TwoSidedLongEdge  | PPD DuplexNoTumble |

 

3. DocumentDuplex オプションの name 属性、PPD. でオプションの名前に一致します。

## <a name="documentnup"></a>DocumentNUp


この機能は、複数のページのコンテンツが物理メディアの各シートに印刷することを指定します。 異なるドキュメントの内容が同じシートに印刷されないように、印刷を行う必要があります。 印刷スキーマの仕様はこのオプションの名前を指定していません。ただし、オプションでは、物理メディアの 1 つの側では、ページの数を指定する ScoredProperty と PagesPerSheet の値をサポートします。 1、2、4、6、8、9、12、16、25、2、6、8、12、および 32 回転されている物理ページの向きで 32 PagesPerSheet の値を指定できます。

選択した N-up に対して生成された PCL6 はフィルターによって決まります。

選択した N-up に対して生成された PostScript はフィルターによって決まります。

**JobOutputBin**

この機能では、印刷デバイスが印刷された後にメディアを格納する場所の場所について説明します。 サポートされているオプションは、対応する GPD/PPD エントリを持つです。

選択した出力トレイ用に生成 PCL6 は GPD OutputBin 機能によって指定されます。 次の順序で使用する、GPD でオプションが選択されます。

1. PrintSchemaKeywordMap を指定しての name 属性と一致するかどうか、\[ジョブ |ドキュメント |ページ\]OutputBin オプション。

2. Name 属性、\[ジョブ |ドキュメント |ページ\]OutputBin オプション、GPD でオプションの名前に一致します。

選択した双方向に対して生成された PostScript は PPD OutputBin 機能によって指定されます。 次の順序で PPD で使用するオプションが選択されます。
1. MSPrintSchemaKeywordMap を指定しての name 属性と一致するかどうか、\[ジョブ |ドキュメント |ページ\]OutputBin オプション。

2. Name 属性、\[ジョブ |ドキュメント |ページ\]OutputBin オプション、PPD. でオプションの名前に一致

## <a name="jobbindalldocuments"></a>JobBindAllDocuments


この機能では、印刷ジョブで印刷された用紙のバインドのメソッドについて説明します。 印刷ジョブのすべてのドキュメントをまとめてバインドする必要があります。 サポートされているオプションは次のとおりです。None、BindBottom、BindLeft、BindRight、BindTop、小冊子、EdgeStitchBottom、EdgeStitchLeft、EdgeStitchRight および EdgeStitchTop します。

小冊子を選択すると、フィルターの出力は再の順序は、半分のページに書籍の適切な順序でジョブ用のシートのスタックを折りたたむときにページを 2 枚として書式設定します。

小冊子の BindingGutter ScoredProperty を指定すると、フィルターは JobBindAllDocumentsGutter パラメーターで指定されたサイズ以上である (からスケールの印刷可能領域の端に用紙のセンター) センター余白を適用します。

ときに、BindLeft BindingGutter ScoredProperty が指定されてまたは EdgeStitchLeft フィルター JobBindAllDocumentsGutter パラメーターで指定された右側に、シートの正面をシフトします。 印刷可能領域を今すぐ外側にある右側にあるコンテンツはクリップされます。 右端 JobBindAllDocumentsGutter パラメーターで指定したとおりに、シートの背面にある上のコンテンツがクリップされます。

BindTop BindingGutter ScoredProperty が指定されて、EdgeStitchTop フィルターは、下部 JobBindAllDocumentsGutter パラメーターで指定されたシートのフロント エンドとバックエンドの辺のコンテンツを移動します。 下部にある印刷可能領域を今すぐ外側にあるコンテンツはクリップされます。

BindRight BindingGutter ScoredProperty が指定されて場合または EdgeStitchRight フィルターは、右側 JobBindAllDocumentsGutter パラメーターで指定されたシートの前面にあるコンテンツをクリップします。 シートの背面にある上のコンテンツは、JobBindAllDocumentsGutter パラメーターで指定した左にシフトされます。 印刷可能領域を今すぐ外側にある左側にあるコンテンツはクリップされます。

BindBottom または EdgeStitchBottom BindingGutter ScoredProperty を指定すると、フィルターは、上部 JobBindAllDocumentsGutter パラメーターで指定されたシートのフロント エンドとバックエンドの辺のコンテンツを移動します。 印刷可能領域を今すぐ外側にある上部のコンテンツはクリップされます。

**注**  綴じ辺は、ジョブの最初のドキュメントの最初のページの向きに基づいて指定されたエッジ。 その他のすべてのオプション、BindingGutter は無視されます。

 

GPD ファイルが選択されているオプションのコマンドを指定しない場合は、フィルターによって選択したバインドに対して生成された PCL6 が決まります。

PPD ファイルが選択したオプションの呼び出しコマンドを指定しない場合は、フィルターによって選択したバインドに対して生成された PostScript が決まります。

## <a name="documentbinding"></a>DocumentBinding


この機能では、印刷ジョブに関連付けられているドキュメントの印刷された用紙をバインドするときに使用する方法について説明します。 ドキュメント内のすべてのページをまとめてバインドする必要があります。 サポートされているオプションは次のとおりです。None、BindBottom、BindLeft、BindRight、BindTop、小冊子、EdgeStitchBottom、EdgeStitchLeft、EdgeStitchRight、および EdgeStitchTop します。

小冊子を選択すると、再の順序は、半分のページに書籍の適切な順序でドキュメントのシートのスタックを折りたたむときにページを使用して、フィルターの出力を 2 枚としてフォーマットされます。

小冊子の BindingGutter ScoredProperty を指定すると、フィルターは DocumentBindingGutter パラメーターで指定されたサイズ以上である (からスケールの印刷可能領域の端に用紙のセンター) センター余白を適用します。

BindLeft または EdgeStitchLeft BindingGutter ScoredProperty が指定されて、フィルター、シートの前面にある DocumentBindingGutter パラメーターで指定された右にシフトします。 印刷可能領域を今すぐ外側にある右側にあるコンテンツはクリップされます。 右端 DocumentBindingGutter パラメーターで指定したとおりに、シートの背面にある上のコンテンツがクリップされます。

BindTop または EdgeStitchTop BindingGutter ScoredProperty を指定すると、フィルターは、下部に DocumentBindingGutter パラメーターで指定されたシートのフロント エンドとバックエンドの辺のコンテンツを移動します。 下部にある印刷可能領域を今すぐ外側にあるコンテンツはクリップされます。

BindRight BindingGutter ScoredProperty が指定されて場合または EdgeStitchRight フィルターは、右側 DocumentBindingGutter パラメーターで指定されたシートの前面にあるコンテンツをクリップします。 シートの背面にある上のコンテンツは、DocumentBindingGutter パラメーターで指定した左にシフトされます。 印刷可能領域を今すぐ外側にある左側にあるコンテンツはクリップされます。

BindBottom または EdgeStitchBottom BindingGutter ScoredProperty を指定すると、フィルターは、上部 DocumentBindingGutter パラメーターで指定されたシートのフロント エンドとバックエンドの辺のコンテンツを移動します。 印刷可能領域を今すぐ外側にある上部のコンテンツはクリップされます。

**注**  綴じ辺は、ドキュメントの最初のページの向きに基づいて指定されたエッジ。 その他のすべてのオプション、BindingGutter は無視されます。

 

GPD ファイルが選択されているオプションのコマンドを指定しない場合は、フィルターによって選択したバインドに対して生成された PCL6 が決まります。

PPD ファイルが選択したオプションの呼び出しコマンドを指定しない場合は、フィルターによって選択したバインドに対して生成された PostScript が決まります。

## <a name="jobstaplealldocuments"></a>JobStapleAllDocuments


この機能は、印刷ジョブで印刷された用紙をステープル処理するときに使用する方法を説明します。 ジョブ内のすべてのドキュメントは、まとめてホチキス止めにする必要があります。 サポートされているオプションは、対応する GPD/PPD エントリで。

選択したホチキス止めの生成 PCL6 は GPD ホチキス止めの機能によって指定されます。 次の順序で使用する、GPD でオプションが選択されます。

1. PrintSchemaKeywordMap が指定されており、JobStapleAllDocuments オプションの名前属性と一致します。

2. JobStapleAllDocuments オプションの name 属性は、GPD でオプションの名前と一致します。

選択したホチキス止めに対して生成された PostScript は JobStapleAllDocuments または DocumentStaple MSPrintSchemaKeywordMap 値を持つ PPD 機能によって指定されます。 次の順序で PPD で使用するオプションが選択されます。
1. MSPrintSchemaKeywordMap が指定されており、JobStapleAllDocuments オプションの名前属性と一致します。

2. JobStapleAllDocuments オプションの name 属性、PPD. でオプションの名前に一致します。

## <a name="jobholepunch"></a>JobHolePunch


この機能は、ときに使用する方法を説明します。 印刷ジョブで印刷された用紙のパンチ穴します。 ジョブのすべてのドキュメントには、一緒にパンチ穴必要があります。 サポートされているオプションは、対応する GPD/PPD エントリで。

選択した穴のパンチ穴を生成する PCL6 は JobHolePunch または DocumentHolePunch PrintSchemaKeywordMap 値を持つ GPD 機能によって指定されます。 次の順序で使用する、GPD でオプションが選択されます。

1. PrintSchemaKeywordMap が指定されており、JobHolePunch オプションの名前属性と一致します。

2. JobHolePunch オプションの name 属性は、GPD でオプションの名前と一致します。

選択した穴のパンチ穴を生成する PostScript は JobHolePunch または DocumentHolePunch MSPrintSchemaKeywordMap 値を持つ PPD 機能によって指定されます。 次の順序で PPD で使用するオプションが選択されます。
1. MSPrintSchemaKeywordMap が指定されており、JobHolePunch オプションの名前属性と一致します。

2. JobHolePunch オプションの name 属性、PPD. でオプションの名前に一致します。

## <a name="documentholepunch"></a>DocumentHolePunch


この機能は、ときに使用する方法を説明します。 印刷ジョブに関連付けられているドキュメントの印刷された用紙のパンチ穴します。 すべてのページ、ドキュメントに一緒にパンチ穴があります。 サポートされているオプションは、対応する GPD/PPD エントリで。

選択した穴のパンチ穴を生成する PCL6 は JobHolePunch または DocumentHolePunch PrintSchemaKeywordMap 値を持つ GPD 機能によって指定されます。 次の順序で使用する、GPD でオプションが選択されます。

1. PrintSchemaKeywordMap が指定されており、DocumentHolePunch オプションの名前属性と一致します。

2. DocumentHolePunch オプションの name 属性は、GPD でオプションの名前と一致します。

選択した穴のパンチ穴を生成する PostScript は JobHolePunch または DocumentHolePunch MSPrintSchemaKeywordMap 値を持つ PPD 機能によって指定されます。 次の順序で PPD で使用するオプションが選択されます。
1. MSPrintSchemaKeywordMap が指定されており、DocumentHolePunch オプションの名前属性と一致します。

2. DocumentHolePunch オプションの name 属性、PPD. でオプションの名前に一致します。

## <a name="pagemirrorimage"></a>PageMirrorImage


この機能は、ページの内容をミラー化するかどうかを指定します。 サポートされているオプションは None と MirrorImageWidth します。

選択したミラーリング用に生成 PCL6 は PageMirrorImage の PrintSchemaKeywordMap 値を持つ GPD 機能によって指定されます。 次の順序で使用する、GPD でオプションが選択されます。

1. PrintSchemaKeywordMap が指定されており、PageMirrorImage オプションの名前属性と一致します。

2. PageMirrorImage オプションの name 属性は、GPD でオプションの名前と一致します。

選択したミラーリング用に生成 PostScript は PPD MirrorPrint 機能によって指定されます。 次の順序で PPD で使用するオプションが選択されます。
1. MSPrintSchemaKeywordMap が指定されており、PageMirrorImage オプションの名前属性と一致します。

2. 次の既定のマッピングが使用されます。

| PageMirrorImage 値        | GPD/PPD ファイルのエントリ |
|------------------------------|--------------------|
| PrintTicket なし             | PPD False          |
| PrintTicket MirrorImageWidth | PPD True           |

 

3. PageMirrorImage オプションの name 属性、PPD. でオプションの名前に一致します。

## <a name="pagenegativeimage"></a>PageNegativeImage


この機能は、そのかどうか、ページのコンテンツが負のイメージをする必要がありますを指定します。 サポートされているオプションは、None と負です。

選択した負の印刷用に生成 PCL6 は PageNegativeImage の PrintSchemaKeywordMap 値を持つ GPD 機能によって指定されます。 次の順序で使用する、GPD でオプションが選択されます。

1. PrintSchemaKeywordMap が指定されており、PageNegativeImage オプションの名前属性と一致します。

2. PageNegativeImage オプションの name 属性は、GPD でオプションの名前と一致します。

選択された負の印刷用に生成された PostScript は PPD NegativePrint 機能によって指定されます。 次の順序で PPD で使用するオプションが選択されます。
1. MSPrintSchemaKeywordMap が指定されており、PageNegativeImage オプションの名前属性と一致します。

2. 次の既定のマッピングが使用されます。

| PageNegativeImage 値 | GPD/PPD ファイルのエントリ |
|-------------------------|--------------------|
| PrintTicket なし        | PPD False          |
| PrintTicket 負の値    | PPD True           |

 

3. PageNegativeImage オプションの name 属性、PPD. でオプションの名前に一致します。

## <a name="related-topics"></a>関連トピック

[PageMediaSize の既定のマッピング](default-pagemediasize-mappings.md)  

[標準的な XPS のフィルター](standard-xps-filters.md)  

印刷スキーマの仕様は、ここでダウンロードできます。

[印刷スキーマ仕様 1.1](http://download.microsoft.com/download/1/6/a/16acc601-1b7a-42ad-8d4e-4f0aa156ec3e/print-schema-spec-1-1.zip)

[印刷スキーマの仕様を 2.0](http://download.microsoft.com/download/d/e/c/deca6e6b-3e81-48e7-b7ef-6d92a547d03c/print-schema-spec-2-0.zip)


