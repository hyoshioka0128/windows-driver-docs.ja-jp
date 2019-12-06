---
title: サポートされている PrintTicket 機能
description: このセクションでは、標準の XPS フィルターでサポートされる PrintTicket 機能について説明します。
ms.assetid: 6D1AD770-D4BA-4BDC-886A-C5C36A09BB0E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20ef6c4698a744ad8efe77655fac2c05854f04e1
ms.sourcegitcommit: 3ee05aabaf9c5e14af56ce5f1dde588c2c7eb4ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74881903"
---
# <a name="supported-printticket-features"></a>サポートされている PrintTicket 機能

このセクションでは、標準の XPS フィルターでサポートされる PrintTicket 機能について説明します。

これらすべての機能は、XPS フィルターが生成された PDL コマンドを変更することによる影響を受けます。 PDL コマンドがフィルター自体によって生成されるか、デバイス GPD/PPD によって指定されているかにかかわらず、これらの機能によって、XPS フィルターが PDL コマンドを変更することがあります。 次のセクションで参照されているすべての要素 (Features、Options、スコア Edproperties、Parameters) は、print schema keywords (psk) 名前空間にあります。

## <a name="pagemediasize"></a>PageMediaSize

この機能は、印刷出力に使用されるメディアシートのサイズを示します。 名前に加えて、各オプションには、MediaSizeWidth と Mediasizewidth という2つのスコア付けされたプロパティを含めることができます。 これらは、メディアの物理サイズを示します。 サポートされているオプションは、対応する GPD/PPD ファイルエントリを持つ任意のオプションです。

PCL6/GPD の場合、PrintTicket オプションが CustomMediaSize の場合、PageMediaSizeMediaSizeWith パラメーターと PageMediaSizeMediaSizeHeight パラメーターを使用してメディアのサイズを取得します。

PostScript/PPD の場合、PrintTicket オプションが PSCustomMediaSize の場合、メディアのサイズを取得するために、PageMediaSizePSHeight パラメーターとパラメーターが使用されます。 選択したメディアの種類に対して生成された PCL6 は、GPD PageSize 機能の値によって指定されます。 次の一覧は、使用する PageMediaSize オプションを決定するために GPD を検査する順序を示しています。

1. PrintSchemaKeywordMap を指定した場合、PageMediaSize オプションの name 属性と一致します。

1. 次の[既定の PageMediaSize マッピング](default-pagemediasize-mappings.md)が使用されます。

1. PageSize オプションの name 属性は、GPD 内のオプションの名前と一致します。

レンダリングプロセス中、任意の GPD コマンドの PhysPaperWidth が、MediaSizeWidth スコアのプロパティまたは PageMediaSizeMediaSizeWidth パラメーターで指定された用紙の幅に置き換えられます。

また、任意の GPD コマンドの PhysPaperLength を、MediaSizeHeight の焦げ Edproperty または PageMediaSizeMediaSizeHeight パラメーターで指定された用紙の長さに置き換えます。

選択したメディアの種類に対して生成された PostScript は、PPD PageSize 機能によって指定されます。 使用する PPD のオプションは、次の順序で選択されます。

1. MSPrintSchemaKeywordMap を指定した場合、PageMediaSize オプションの name 属性と一致します。

1. PageSize オプションの name 属性は、PPD のオプションの名前と一致します。

## <a name="pagemediatype"></a>PageMediaType

この機能では、デバイスで使用できるメディアシートの特性 (coatings、メディアマテリアル、メディアの重さなど) が説明されています。 サポートされているオプションは、対応する GPD/PPD エントリを持つものです。

選択したメディアの種類に対して生成された PCL6 は、GPD MediaType 機能によって指定されます。 使用する GPD のオプションは、次の順序で選択されます。

1. PrintSchemaKeywordMap を指定した場合、PageMediaType オプションの name 属性と一致します。

1. 次の既定のマッピングが使用されます。

    | PageMediaType 値            | GPD/PPD ファイルエントリ |
    |--------------------------------|--------------------|
    | PrintTicket PhotographicGlossy | GPD 光沢         |
    | PrintTicket Plain              | GPD 標準       |
    | PrintTicket の透明度       | GPD の透明度   |

1. PageMediaType オプションの name 属性は、GPD のオプションの名前と一致します。

選択したメディアの種類に対して生成された PostScript は、PPD MediaType 機能によって指定されます。 使用する PPD のオプションは、次の順序で選択されます。

1. MSPrintSchemaKeywordMap を指定した場合、PageMediaType オプションの name 属性と一致します。

1. PageMediaType オプションの name 属性は、PPD のオプションの名前と一致します。

## <a name="pagemediacolor"></a>PageMediaColor

この機能は、メディアシートの色について説明します。 サポートされているオプションは、対応する GPD/PPD エントリを持つものです。

選択したメディアの色に対して生成される PCL6 は、PrintSchemaKeywordMap: "PageMediaColor" という \*を含む GPD 機能によって指定されます。 使用する GPD のオプションは、次の順序で選択されます。

1. PrintSchemaKeywordMap を指定した場合、PageMediaColor オプションの name 属性と一致します。

1. PageMediaColor オプションの name 属性は、GPD のオプションの名前と一致します。

選択したメディアの色に対して生成される PostScript は、PPD MediaColor 機能によって指定されます。 使用する PPD のオプションは、次の順序で選択されます。

1. MSPrintSchemaKeywordMap を指定した場合、PageMediaColor オプションの name 属性と一致します。

1. PageMediaColor オプションの name 属性は、PPD のオプションの名前と一致します。

## <a name="jobinputbin"></a>JobInputBin

この機能では、メディアを印刷デバイスに取り込む入力場所について説明します。 サポートされているオプションは、対応する GPD/PPD エントリを持つオプションです。

選択した入力トレイ用に生成された PCL6 は、GPD InputBin 機能によって指定されます。 使用する GPD のオプションは、次の順序で選択されます。

1. PrintSchemaKeywordMap を指定した場合、JobInputBin オプションの name 属性と一致します。

1. 次の既定のマッピングが使用されます。

    | JobInputBin 値      | GPD/PPD ファイルエントリ                  |
    |------------------------|-------------------------------------|
    | PrintTicket カセット   | GPD AUTO、カセット、ENVFEED、ENVMANUAL |
    | PrintTicket の自動の自動で | GPD FORMSOURCE                      |
    | PrintTicket High       | GPD LARGECAPACITY、LARGEFMT、LOWER    |
    | PrintTicket の手動     | GPD MANUAL、中段、SMALLFMT          |
    | PrintTicket トラクター    | GPD トラクター、UPPER                   |

1. PageMediaType オプションの name 属性は、GPD のオプションの名前と一致します。

選択した入力トレイ用に生成された PostScript は、PPD InputSlot 機能によって指定されます。 使用する PPD のオプションは、次の順序で選択されます。

1. MSPrintSchemaKeywordMap を指定した場合、JobInputBin オプションの name 属性と一致します。

1. JobInputBin オプションの name 属性は、PPD のオプションの名前と一致します。

## <a name="pageorientation"></a>PageOrientation

この機能は、コンテンツの座標空間からシートのメディア座標空間に変換するときに使用する回転変換を示します。 サポートされているオプションは、縦、横、ReversePortrait、および ReverseLandscape です。

選択した方向に対して生成された PCL6 は、GPD Orientation 機能によって指定されます。 使用する GPD のオプションは、次の順序で選択されます。

1. PrintSchemaKeywordMap を指定した場合、PageOrientation オプションの name 属性と一致します。

1. 次の既定のマッピングが使用されます。

    | PageOrientation 値        | GPD/PPD ファイルエントリ   |
    |------------------------------|----------------------|
    | PrintTicket 縦長         | GPD 縦         |
    | PrintTicket の横        | GPD ランドスケープ\_CC90  |
    | PrintTicket ReverseLandscape | GPD ランドスケープ\_CC 1.0 |

1. PageOrientation オプションの name 属性は、GPD 内のオプションの名前と一致します。

選択した向きに対して生成される PostScript は、フィルターによって決まります。

## <a name="pageoutputcolor"></a>PageOutputColor

この機能は、出力先ドキュメントページの印刷出力の色特性 (色、モノクロ) を制御します。 サポートされているオプションは、Color、グレースケール、モノクロです。

選択した出力色に対して生成された PCL6 は、GPD ColorMode 機能によって指定されます。 使用する GPD のオプションは、次の順序で選択されます。

1. PrintSchemaKeywordMap を指定した場合、PageOutputColor オプションの name 属性と一致します。

1. PageOutputColor オプションの name 属性は、GPD 内のオプションの名前と一致します。

選択した出力色に対して生成される PostScript は、フィルターによって決定されます。

## <a name="pageresolution"></a>PageResolution 方法

この機能では、デバイスが出力を生成できる解像度 (1 インチあたりのドット数) を定義します。 印刷スキーマでは、この機能のオプションに標準名は指定されていません。ただし、オプション名 (解像度 x) と解像度 y に関係なく、2つのスコアプロパティをサポートしています。 サポートされているオプションは、対応する GPD/PPD エントリを持つものです。

選択した解像度に対して生成された PCL6 は、GPD Resolution 機能によって指定されます。 使用する GPD のオプションは、次の順序で選択されます。

1. PrintSchemaKeywordMap を指定した場合に、PageResolution オプションの name 属性と一致します。

1. PageResolution オプションの name 属性は、このオプションの名前と一致します。

レンダリング時には、任意の GPD コマンドの GraphicsXRes と TextXRes が、解像度 x で指定された水平方向の解像度に置き換えられます。
また、GPD コマンドの GraphicsYRes と TextYRes も、解決方法 y で指定された垂直方向の解像度に置き換えられます。

選択した解像度に対して生成された PostScript は、PPD 解像度または JCLResolution 機能によって指定されます。 使用する PPD のオプションは、次の順序で選択されます。

1. MSPrintSchemaKeywordMap を指定した場合に、PageResolution オプションの name 属性と一致します。

1. PageResolution 検索オプションの name 属性は、PPD のオプションの名前と一致します。

## <a name="pageoutputquality"></a>PageOutputQuality

この機能は、ドキュメントページの印刷品質を定義します。 サポートされているオプションは、対応する GPD/PPD エントリを持つオプションです。

選択した品質に対して生成された PCL6 は、GPD 機能によって、PrintSchemaKeywordMap の値が PageOutputQuality によって指定されます。 使用する GPD のオプションは、次の順序で選択されます。

1. PrintSchemaKeywordMap を指定した場合、PageOutputQuality オプションの name 属性と一致します。

1. PageOutputQuality オプションの name 属性は、GPD 内のオプションの名前と一致します。

選択した品質に対して生成される PostScript は、MSPrintSchemaKeywordMap 値が PageOutputQuality である PPD 機能によって指定されます。 使用する PPD のオプションは、次の順序で選択されます。

1. MSPrintSchemaKeywordMap を指定した場合、PageOutputQuality オプションの name 属性と一致します。

1. PageOutputQuality オプションの name 属性は、PPD のオプションの名前と一致します。

## <a name="jobcopiesalldocuments"></a>JobCopiesAllDocuments

このパラメーターは、印刷ジョブ内のすべてのドキュメントを出力する回数を指定します。

選択したコピーに対して生成された PCL6 は、フィルターによって決定されます。 このパラメーターとの対話については、JobCollateAllDocuments 機能に関する説明を参照してください。

選択したコピーに対して生成される PostScript は、フィルターによって決定されます。 このパラメーターとの対話については、JobCollateAllDocuments 機能に関する説明を参照してください。

## <a name="documentcopiesallpages"></a>DocumentCopiesAllPages

このパラメーターは、印刷ジョブに関連付けられたドキュメントが出力するページコピーの数を指定します。

選択したコピーに対して生成された PCL6 は、フィルターによって決定されます。 このパラメーターと対話するには、DocumentCollate 機能を参照してください。

選択したコピーに対して生成される PostScript は、フィルターによって決定されます。 このパラメーターと対話するには、DocumentCollate 機能を参照してください。

## <a name="pagecopies"></a>PageCopies

このパラメーターは、ドキュメント内の個々のソースドキュメントページのコピーを出力する回数を指定します。 コピー数は現在のページにのみ適用されるため、照合順序はありません。

選択したコピーに対して生成された PCL6 は、フィルターによって決定されます。

選択したコピーに対して生成される PostScript は、フィルターによって決定されます。

## <a name="documentcollate"></a>DocumentCollate

この機能は、印刷ジョブに関連付けられているドキュメントのページを印刷出力に表示する順序を指定します。 サポートされているオプションは、照合と丁合いなしです。

選択した照合順序に対して生成された PCL6 は、GPD Collate 機能によって指定されます。 使用する GPD のオプションは、次の順序で選択されます。

1. PrintSchemaKeywordMap を指定した場合、DocumentCollate オプションの name 属性と一致します。

1. 次の既定のマッピングが使用されます。

    | DocumentCollate の値  | GPD/PPD ファイルエントリ |
    |------------------------|--------------------|
    | PrintTicket 丁合いなし | GPD OFF            |
    | PrintTicket の照合   | GPD             |

1. DocumentCollate オプションの name 属性は、GPD 内のオプションの名前と一致します。

> [!NOTE]
> DocumentCollate が丁合いに設定されていて、GPD Collate オプションにコマンドが含まれている場合は、デバイスが照合されたコピーを生成できると想定されます。 *PCL6*フィルターはジョブのコピーを1つだけ生成し、GPD コマンドを使用して、照合されたコピーを生成するようにデバイスに指示します。 フィルターは、GPD コマンドの NumOfCopies を、JobCopiesAllDocuments によって指定されたコピーの数に置き換えます。

選択した照合順序に対して生成された PostScript は、PPD Collate 機能によって指定されます。 使用する PPD のオプションは、次の順序で選択されます。

1. MSPrintSchemaKeywordMap を指定した場合、DocumentCollate オプションの name 属性と一致します。

1. 次の既定のマッピングが使用されます。

    | DocumentCollate の値  | GPD/PPD ファイルエントリ |
    |------------------------|--------------------|
    | PrintTicket 丁合いなし | PPD False          |
    | PrintTicket の照合   | PPD True           |

1. DocumentCollate オプションの name 属性は、PPD のオプションの名前と一致します。

> [!NOTE]
> DocumentCollate が丁合いに設定されていて、PPD に Collate 機能が含まれている場合、または DocumentCollate にマップされたキーワードである機能がある場合は、デバイスが照合されたコピーを生成できることを前提としています。 XPS.PS フィルターは、ジョブのコピーを1つだけ生成し、PPD コマンドを使用して、照合されたコピーを生成するようにデバイスに指示します。

## <a name="jobduplexalldocumentscontiguously"></a>JobDuplexAllDocumentsContiguously

この機能は、ドキュメントの境界を考慮せずに印刷ジョブの両面印刷を指定します。 両面印刷が指定されている場合、印刷ジョブ内のすべてのドキュメントのすべてのページは、ドキュメント間に空白ページを挿入せずに、常に二重に印刷されます。 サポートされているオプションは、OneSided、TwoSidedShortEdge、および TwoSidedLongEdge です。

選択した二重に対して生成された PCL6 は、GPD デュプレックス機能によって指定されます。 使用する GPD のオプションは、次の順序で選択されます。

1. PrintSchemaKeywordMap を指定した場合、JobDuplexAllDocumentsContiguously オプションの name 属性と一致します。

1. 次の既定のマッピングが使用されます。

    | JobDuplexAllDocumentsContiguously 値 | GPD/PPD ファイルエントリ |
    |-----------------------------------------|--------------------|
    | PrintTicket OneSided                    | GPD NONE           |
    | PrintTicket TwoSidedShortEdge           | GPD 横線     |
    | PrintTicket TwoSidedLongEdge            | GPD VERTICAL       |

1. JobDuplexAllDocumentsContiguously オプションの name 属性は、GPD のオプションの名前と一致します。

選択した二重用に生成された PostScript は、[使用する PPD] のオプションが次の順序で選択されます。

1. MSPrintSchemaKeywordMap を指定した場合、JobDuplexAllDocumentsContiguously オプションの name 属性と一致します。

1. 次の既定のマッピングが使用されます。

    | JobDuplexAllDocumentsContiguously 値 | GPD/PPD ファイルエントリ |
    |-----------------------------------------|--------------------|
    | PrintTicket OneSided                    | [PPD None]           |
    | PrintTicket TwoSidedShortEdge           | PPD duplextumum   |
    | PrintTicket TwoSidedLongEdge            | PPD DuplexNoTumble |

1. JobDuplexAllDocumentsContiguously オプションの name 属性は、PPD のオプションの名前と一致します。

## <a name="documentduplex"></a>DocumentDuplex

この機能は、印刷ジョブの関連ドキュメントの両面印刷を制御します。 これが指定されている場合、印刷される出力は、メディアの新しいシートの前面から開始されます。 サポートされているオプションは、OneSided、TwoSidedShortEdge、および TwoSidedLongEdge です。

選択した二重に対して生成された PCL6 は、GPD デュプレックス機能によって指定されます。 使用する GPD のオプションは、次の順序で選択されます。

1. PrintSchemaKeywordMap を指定した場合、DocumentDuplex オプションの name 属性と一致します。

1. 次の既定のマッピングが使用されます。

    | DocumentDuplex 値          | GPD/PPD ファイルエントリ |
    |-------------------------------|--------------------|
    | PrintTicket OneSided          | GPD NONE           |
    | PrintTicket TwoSidedShortEdge | GPD 横線     |
    | PrintTicket TwoSidedLongEdge  | GPD VERTICAL       |

1. DocumentDuplex オプションの name 属性は、GPD 内のオプションの名前と一致します。

選択した双方向用に生成された PostScript は、PPD 二重機能によって指定されます。 使用する PPD のオプションは、次の順序で選択されます。

1. MSPrintSchemaKeywordMap を指定した場合、DocumentDuplex オプションの name 属性と一致します。

1. 次の既定のマッピングが使用されます。

    | DocumentDuplex 値          | GPD/PPD ファイルエントリ |
    |-------------------------------|--------------------|
    | PrintTicket OneSided          | [PPD None]           |
    | PrintTicket TwoSidedShortEdge | PPD duplextumum   |
    | PrintTicket TwoSidedLongEdge  | PPD DuplexNoTumble |

1. DocumentDuplex オプションの name 属性は、PPD のオプションの名前と一致します。

## <a name="documentnup"></a>DocumentNUp

この機能では、複数ページのコンテンツを物理メディアの各シートに印刷するように指定します。 また、印刷は、異なるドキュメントのコンテンツが同じシートに印刷されないように行う必要があります。 印刷スキーマの仕様では、このオプションの名前は指定されていません。ただし、このオプションでは、物理メディアの片面に配置されるページ数を指定する、スコア付け Edproperty とページ Persheet の値がサポートされています。 ページ Persheet のサポートされている値は1、2、4、6、8、9、12、16、25、32で、物理的なページの向きが2、6、8、12、および32に回転しています。

選択した N アップに対して生成された PCL6 は、フィルターによって決定されます。

選択した N-up 用に生成された PostScript は、フィルターによって決定されます。

### <a name="joboutputbin"></a>JobOutputBin

この機能は、印刷後にメディアが格納される印刷デバイス上の場所を示します。 サポートされているオプションは、対応する GPD/PPD エントリを持つオプションです。

選択した出力ビンに対して生成された PCL6 は、GPD OutputBin 機能によって指定されます。 使用する GPD のオプションは、次の順序で選択されます。

1. PrintSchemaKeywordMap が指定されていて、\[Job | の name 属性と一致する場合は、Document |ページ\]OutputBin オプション。

1. \[Job | の name 属性 |Document |ページ\]OutputBin オプションは、GPD のオプションの名前と一致します。

選択した二重用に生成された PostScript は、PPD OutputBin 機能によって指定されます。 使用する PPD のオプションは、次の順序で選択されます。

1. MSPrintSchemaKeywordMap が指定されていて、\[Job | の name 属性と一致する場合は、Document |ページ\]OutputBin オプション。

1. \[Job | の name 属性 |Document |ページ\]OutputBin オプションは、PPD のオプションの名前と一致します。

## <a name="jobbindalldocuments"></a>JobBindAllDocuments

この機能は、印刷ジョブで印刷されるシートにバインドする方法について説明します。 印刷ジョブのすべてのドキュメントを結合する必要があります。 サポートされているオプションは、None、BindBottom、Bindbottom、BindRight、Bindbottom、小冊子、EdgeStitchBottom、EdgeStitchLeft、EdgeStitchRight、および EdgeStitchTop です。

[小冊子] が選択されている場合、フィルターの出力は2つの形式に設定されています。これにより、ジョブのシートのスタックが1つのページのうち半分に折りたたまれたときに、そのページがブックの正しい順序になります。

[小冊子] に BindingGutter のスコアが指定されている場合、フィルターによって、Jobbindallpaper margin パラメーターで指定されたサイズ以上の中央余白 (用紙の中央から拡大可能な領域の端まで) が適用されます。

[BindLeft] に BindingGutter の "Edproperty" を指定した場合、または EdgeStitchLeft フィルターを使用すると、Jobbindall パラメーターで指定したとおりに、シートの前面が右側に移動します。 右側のコンテンツは、印刷可能領域の外側に表示されます。 シートの背面のコンテンツは、Jobbindallsheet パラメーターで指定された右端にクリップされます。

BindTop に BindingGutter を指定すると、EdgeStitchTop は、ワークシートの前面と裏面の両方の内容を、Jobbindall パラメーターで指定された下部に移動します。 現在、印刷可能領域の外側にあるコンテンツはクリップされます。

BindRight または EdgeStitchRight に BindingGutter の値 Edproperty が指定されている場合、フィルターは Jobbindall パラメーターで指定された右側のシートの前面にコンテンツをクリップします。 シートの背面のコンテンツは、Jobbindallsheet パラメーターで指定されているように左にシフトされます。 左側のコンテンツは、印刷可能領域の外にある内容がクリップされます。

BindBottom または EdgeStitchBottom に BindingGutter の焦げ Edproperty が指定されている場合、フィルターは、Jobbindall パラメーターで指定されているように、シートの前面と裏面の両方の内容を一番上に移動します。 上部に印刷可能領域の外側にあるコンテンツはクリップされます。

> [!NOTE]
> バインドエッジは、ジョブ内の最初のドキュメントの最初のページの向きに基づいて指定されたエッジです。 その他のオプションについては、BindingGutter は無視されます。

GPD ファイルで、選択したオプションのコマンドが指定されていない場合は、選択したバインドに対して生成された PCL6 がフィルターによって決定されます。

選択したオプションの呼び出しコマンドが PPD ファイルによって指定されていない場合、選択したバインドに対して生成される PostScript はフィルターによって決定されます。

## <a name="documentbinding"></a>DocumentBinding

この機能は、印刷ジョブに関連付けられているドキュメントの印刷シートをバインドするときに使用する方法について説明します。 ドキュメント内のすべてのページを結合する必要があります。 サポートされているオプションは、None、BindBottom、Bindbottom、BindRight、Bindbottom、小冊子、EdgeStitchBottom、EdgeStitchLeft、EdgeStitchRight、および EdgeStitchTop です。

[小冊子] を選択すると、フィルターの出力は2つの形式になり、ページが並べ替えられます。これにより、ドキュメントのシートのスタックが、1つのブックに対して適切な順序で折りたたまれます。

"小冊子" に BindingGutter の焦げ Edproperty が指定されている場合、フィルターにより、DocumentBindingGutter パラメーターで指定されているサイズ以上の中央余白 (用紙の中央から拡大可能な領域の端まで) が適用されます。

BindLeft または EdgeStitchLeft に BindingGutter の値 Edproperty が指定されている場合、フィルターは DocumentBindingGutter パラメーターで指定されているとおりに、シートのフロントサイドを右に移動します。 右側のコンテンツは、印刷可能領域の外側に表示されます。 シートの背面のコンテンツは、DocumentBindingGutter パラメーターで指定された右端にクリップされます。

BindTop または EdgeStitchTop に BindingGutter の値 Edproperty が指定されている場合、フィルターは、シートの前面と裏面の両方の内容を DocumentBindingGutter パラメーターで指定された下部に移動します。 現在、印刷可能領域の外側にあるコンテンツはクリップされます。

BindRight または EdgeStitchRight に BindingGutter の焦げ Edproperty が指定されている場合、DocumentBindingGutter パラメーターで指定されているとおり、フィルターによって右側のシートの前面にコンテンツがクリップされます。 シートの背面のコンテンツは、DocumentBindingGutter パラメーターで指定されているように左にシフトされます。 左側のコンテンツは、印刷可能領域の外にある内容がクリップされます。

BindBottom または EdgeStitchBottom に BindingGutter の "Edproperty" が指定されている場合、フィルターは DocumentBindingGutter パラメーターで指定されているように、シートの前面と裏面の両方の内容を一番上に移動します。 上部に印刷可能領域の外側にあるコンテンツはクリップされます。

> [!NOTE]
> バインドエッジは、ドキュメントの最初のページの向きに基づいて指定されたエッジです。 その他のオプションについては、BindingGutter は無視されます。

GPD ファイルで、選択したオプションのコマンドが指定されていない場合は、選択したバインドに対して生成された PCL6 がフィルターによって決定されます。

選択したオプションの呼び出しコマンドが PPD ファイルによって指定されていない場合、選択したバインドに対して生成される PostScript はフィルターによって決定されます。

## <a name="jobstaplealldocuments"></a>Jobのすべてのドキュメント

この機能は、印刷ジョブで印刷したシートをホチキス止めするときに使用する方法について説明します。 ジョブ内のすべてのドキュメントを一緒にホチキス止めする必要があります。 サポートされているオプションは、対応する GPD/PPD エントリを持つものです。

選択したホチキス止め用に生成された PCL6 は、GPD ホチキス止め機能によって指定されます。 使用する GPD のオプションは、次の順序で選択されます。

1. 場合 PrintSchemaKeywordMap が指定されている場合は、Job の名前属性と一致します。

1. JobGPD の name 属性は、このオプションの名前と一致します。

選択したホチキス止め用に生成された PostScript は、MSPrintSchemaKeywordMap の値が Job に指定された PPD 機能によって指定されます。 使用する PPD のオプションは、次の順序で選択されます。

1. 場合 MSPrintSchemaKeywordMap が指定されている場合は、Job の名前属性と一致します。

1. Jobている Alldocuments オプションの name 属性は、PPD のオプションの名前と一致します。

## <a name="jobholepunch"></a>JobHolePunch

この機能では、印刷ジョブに穴を印刷するときに使用する方法について説明します。 ジョブ内のすべてのドキュメントにパンチ穴をあけする必要があります。 サポートされているオプションは、対応する GPD/PPD エントリを持つものです。

選択した穴あけ用に生成された PCL6 は、GPD 機能で PrintSchemaKeywordMap 値 JobHolePunch または DocumentHolePunch によって指定されます。 使用する GPD のオプションは、次の順序で選択されます。

1. PrintSchemaKeywordMap を指定した場合、JobHolePunch オプションの name 属性と一致します。

1. JobHolePunch オプションの name 属性は、GPD のオプションの名前と一致します。

選択した穴あけ用に生成された PostScript は、MSPrintSchemaKeywordMap 値が JobHolePunch または DocumentHolePunch の PPD 機能によって指定されます。 使用する PPD のオプションは、次の順序で選択されます。

1. MSPrintSchemaKeywordMap を指定した場合、JobHolePunch オプションの name 属性と一致します。

1. JobHolePunch オプションの name 属性は、PPD のオプションの名前と一致します。

## <a name="documentholepunch"></a>DocumentHolePunch

この機能は、印刷ジョブに関連付けられているドキュメントの印刷シートをパンチ穴にパンチするときに使用する方法について説明します。 ドキュメント内のすべてのページがパンチ穴に穴をあけている必要があります。 サポートされているオプションは、対応する GPD/PPD エントリを持つものです。

選択した穴あけ用に生成された PCL6 は、GPD 機能で PrintSchemaKeywordMap 値 JobHolePunch または DocumentHolePunch によって指定されます。 使用する GPD のオプションは、次の順序で選択されます。

1. PrintSchemaKeywordMap を指定した場合、DocumentHolePunch オプションの name 属性と一致します。

1. DocumentHolePunch オプションの name 属性は、GPD のオプションの名前と一致します。

選択した穴あけ用に生成された PostScript は、MSPrintSchemaKeywordMap 値が JobHolePunch または DocumentHolePunch の PPD 機能によって指定されます。 使用する PPD のオプションは、次の順序で選択されます。

1. MSPrintSchemaKeywordMap を指定した場合、DocumentHolePunch オプションの name 属性と一致します。

1. DocumentHolePunch オプションの name 属性は、PPD のオプションの名前と一致します。

## <a name="pagemirrorimage"></a>PageMirrorImage

この機能は、ページコンテンツをミラー化する必要があるかどうかを指定します。 サポートされているオプションは None と MirrorImageWidth です。

選択したミラーリング用に生成された PCL6 は、GPD 機能で PrintSchemaKeywordMap 値が PageMirrorImage によって指定されます。 使用する GPD のオプションは、次の順序で選択されます。

1. PrintSchemaKeywordMap を指定した場合、PageMirrorImage オプションの name 属性と一致します。

1. PageMirrorImage オプションの name 属性は、GPD のオプションの名前と一致します。

選択したミラーリング用に生成された PostScript は、PPD MirrorPrint 機能によって指定されます。 使用する PPD のオプションは、次の順序で選択されます。

1. MSPrintSchemaKeywordMap を指定した場合、PageMirrorImage オプションの name 属性と一致します。

1. 次の既定のマッピングが使用されます。

    | PageMirrorImage 値        | GPD/PPD ファイルエントリ |
    |------------------------------|--------------------|
    | PrintTicket なし             | PPD False          |
    | PrintTicket MirrorImageWidth | PPD True           |

1. PageMirrorImage オプションの name 属性は、PPD のオプションの名前と一致します。

## <a name="pagenegativeimage"></a>PageNegativeImage

この機能は、ページコンテンツがネガイメージである必要があるかどうかを指定します。 サポートされているオプションは None と負です。

選択した否定印刷用に生成された PCL6 は、GPD 機能で PrintSchemaKeywordMap 値 PageNegativeImage を使用して指定されます。 使用する GPD のオプションは、次の順序で選択されます。

1. PrintSchemaKeywordMap を指定した場合、PageNegativeImage オプションの name 属性と一致します。

1. PageNegativeImage オプションの name 属性は、GPD のオプションの名前と一致します。

選択したネガ印刷用に生成された PostScript は、PPD NegativePrint 機能によって指定されます。 使用する PPD のオプションは、次の順序で選択されます。

1. MSPrintSchemaKeywordMap を指定した場合、PageNegativeImage オプションの name 属性と一致します。

1. 次の既定のマッピングが使用されます。

    | PageNegativeImage 値 | GPD/PPD ファイルエントリ |
    |-------------------------|--------------------|
    | PrintTicket なし        | PPD False          |
    | PrintTicket 負の値    | PPD True           |

1. PageNegativeImage オプションの name 属性は、PPD のオプションの名前と一致します。

## <a name="related-topics"></a>関連トピック

[既定の PageMediaSize マッピング](default-pagemediasize-mappings.md)  

[標準の XPS フィルター](standard-xps-filters.md)  

印刷スキーマの仕様は、次の場所でダウンロードできます。

[印刷スキーマの仕様1.1](https://download.microsoft.com/download/1/6/a/16acc601-1b7a-42ad-8d4e-4f0aa156ec3e/print-schema-spec-1-1.zip)

[印刷スキーマの仕様2.0](https://download.microsoft.com/download/d/e/c/deca6e6b-3e81-48e7-b7ef-6d92a547d03c/print-schema-spec-2-0.zip)
