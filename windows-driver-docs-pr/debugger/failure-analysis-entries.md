---
title: エラー分析エントリ
description: DebugFailureAnalysis オブジェクトには、エラー分析エントリのコレクションが含まれています。
ms.assetid: 759DE159-F2A8-4BB1-AAF5-B2B91C4F91B0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b87a01c4d49daff9981a95c6dcd8315056a72370
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826418"
---
# <a name="failure-analysis-entries"></a>エラー分析エントリ


[**Debugfailureanalysis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)オブジェクトには、エラー分析エントリのコレクションが含まれています。 詳細については、「[エラー分析のエントリ、タグ、およびデータ型](writing-an-analysis-extension-to-extend--analyze.md#failure-analysis-entries-tags-and-data-types)」を参照してください。

*エラー分析エントリ*( *FA エントリ*とも呼ばれます) は、次のいずれかになります。

-   [**FA\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/ns-extsfns-_fa_entry)の構造
-   データブロックが続く[**FA\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/ns-extsfns-_fa_entry)構造

[**FA\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/ns-extsfns-_fa_entry)構造の**DataSize**メンバーは、データブロックのサイズ (バイト単位) を保持します。 データブロックがない場合、 **DataSize**は0に等しくなります。 **Fa\_エントリ**構造の**タグ**メンバーは、fa エントリに格納されている情報の種類を識別します。 たとえば、タグ**DEBUG\_FLR\_バグチェック\_コード**は、 **FA\_エントリ**のデータブロックがバグチェックコードを保持することを示します。

場合によっては、データブロックは必要ありません。すべての情報は、タグによって伝達されます。 たとえば、タグ**DEBUG\_FLR\_カーネル\_検証\_ツールが有効になっ**ている[**FA\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/ns-extsfns-_fa_entry)には、データブロックがありません。

各タグは、 [**FA\_ENTRY\_TYPE 列挙型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/ne-extsfns-_fa_entry_type)のいずれかのデータ型に関連付けられています。 たとえば、タグ**debug\_FLR\_バグチェック\_コード**は、データ型**debug\_FA\_ENTRY\_ULONG**に関連付けられています。 タグのデータ型を特定するには、 [IDebugFAEntryTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfaentrytags)インターフェイスの[**GetType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nf-extsfns-idebugfaentrytags-gettype)メソッドを呼び出します。

FA エントリのデータブロックを取得または設定するには、 [**IDebugFailureAnalysis2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)インターフェイスを使用します。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[拡張用の分析拡張機能プラグインを記述しています。](writing-an-analysis-extension-to-extend--analyze.md)

[**FA\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/ns-extsfns-_fa_entry)

 

 






