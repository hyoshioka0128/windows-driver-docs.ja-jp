---
title: エラー分析エントリ
description: DebugFailureAnalysis オブジェクトには、エラーの分析のエントリのコレクションがあります。
ms.assetid: 759DE159-F2A8-4BB1-AAF5-B2B91C4F91B0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1827ec250381d96a06f72955f679ecf7ec4fd25a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580145"
---
# <a name="failure-analysis-entries"></a>エラー分析エントリ


A [ **DebugFailureAnalysis** ](https://msdn.microsoft.com/library/windows/hardware/jj983405)オブジェクトがエラーの分析のエントリのコレクション。 詳細については、[エラー分析のエントリ、タグ、およびデータ型](writing-an-analysis-extension-to-extend--analyze.md#failure-analysis-entries-tags-and-data-types)を参照してください。

A*エラー分析のエントリ*(とも呼ばれる、 *FA エントリ*) は、次のいずれか。

-   [ **FA\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/jj991808)構造体
-   [ **FA\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/jj991808)構造にデータ ブロックを続ける

**DataSize**のメンバー、 [ **FA\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/jj991808)構造体は、データ ブロックのバイト単位のサイズを保持します。 データのブロックが存在しない場合**DataSize**が 0 です。 **タグ**のメンバー、 **FA\_エントリ**構造 FA エントリに格納されている情報の種類を識別します。 タグなど**デバッグ\_FLR\_バグチェック\_コード**データ ブロックのことを示します、 **FA\_エントリ**バグ チェックのコードを保持します。

場合によってはデータ ブロックの必要はありません。すべての情報を伝達するには、タグを使用しています。 たとえば、 [ **FA\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/jj991808)タグを持つ**デバッグ\_FLR\_カーネル\_VERIFIER\_有効**データ ブロックがありません。

各タグは内のデータ型のいずれかに関連付け、 [ **FA\_エントリ\_型**](https://msdn.microsoft.com/library/windows/hardware/jj991809)列挙体。 たとえば、タグ**デバッグ\_FLR\_バグチェック\_コード**データ型に関連付けられた**デバッグ\_FA\_エントリ\_ULONG**. タグのデータ型を確認するのには、呼び出し、 [ **GetType** ](https://msdn.microsoft.com/library/windows/hardware/jj991813)のメソッド、 [IDebugFAEntryTags](https://msdn.microsoft.com/library/windows/hardware/jj983404)インターフェイス。

取得または FA のエントリのデータ ブロックを設定しを使用して、 [ **IDebugFailureAnalysis2** ](https://msdn.microsoft.com/library/windows/hardware/jj983405)インターフェイス。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[分析の拡張機能プラグインを拡張する記述! 分析](writing-an-analysis-extension-to-extend--analyze.md)

[**FA\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/jj991808)

 

 






