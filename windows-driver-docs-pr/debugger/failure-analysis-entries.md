---
title: エラー分析エントリ
description: DebugFailureAnalysis オブジェクトには、エラーの分析のエントリのコレクションがあります。
ms.assetid: 759DE159-F2A8-4BB1-AAF5-B2B91C4F91B0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 976d5ce21c7ce92c7e452974669bb5d45422ae39
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366831"
---
# <a name="failure-analysis-entries"></a>エラー分析エントリ


A [ **DebugFailureAnalysis** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfailureanalysis2)オブジェクトがエラーの分析のエントリのコレクション。 詳細については、次を参照してください。[エラー分析のエントリ、タグ、およびデータ型](writing-an-analysis-extension-to-extend--analyze.md#failure-analysis-entries-tags-and-data-types)します。

A*エラー分析のエントリ*(とも呼ばれる、 *FA エントリ*) は、次のいずれか。

-   [ **FA\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/ns-extsfns-_fa_entry)構造体
-   [ **FA\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/ns-extsfns-_fa_entry)構造にデータ ブロックを続ける

**DataSize**のメンバー、 [ **FA\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/ns-extsfns-_fa_entry)構造体は、データ ブロックのバイト単位のサイズを保持します。 データのブロックが存在しない場合**DataSize**が 0 です。 **タグ**のメンバー、 **FA\_エントリ**構造 FA エントリに格納されている情報の種類を識別します。 タグなど**デバッグ\_FLR\_バグチェック\_コード**データ ブロックのことを示します、 **FA\_エントリ**バグ チェックのコードを保持します。

場合によってはデータ ブロックの必要はありません。すべての情報を伝達するには、タグを使用しています。 たとえば、 [ **FA\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/ns-extsfns-_fa_entry)タグを持つ**デバッグ\_FLR\_カーネル\_VERIFIER\_有効**データ ブロックがありません。

各タグは内のデータ型のいずれかに関連付け、 [ **FA\_エントリ\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/ne-extsfns-_fa_entry_type)列挙体。 たとえば、タグ**デバッグ\_FLR\_バグチェック\_コード**データ型に関連付けられた**デバッグ\_FA\_エントリ\_ULONG**. タグのデータ型を確認するのには、呼び出し、 [ **GetType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nf-extsfns-idebugfaentrytags-gettype)のメソッド、 [IDebugFAEntryTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfaentrytags)インターフェイス。

取得または FA のエントリのデータ ブロックを設定しを使用して、 [ **IDebugFailureAnalysis2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfailureanalysis2)インターフェイス。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[分析の拡張機能プラグインを拡張する記述! 分析](writing-an-analysis-extension-to-extend--analyze.md)

[**FA\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/ns-extsfns-_fa_entry)

 

 






