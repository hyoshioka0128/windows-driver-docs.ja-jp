---
title: 構成形式の改善
description: カウントおよび句読点の代替コピーを制御することに、v4 プリンター ドライバーで書式の設定が改善されました。
ms.assetid: 66FC6BAF-26DD-4E18-B8C9-0BF494346917
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44c02b747e7f86229cea1fb608cf23178d474553
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390578"
---
# <a name="improvements-in-configuration-formats"></a>構成形式の改善


カウントおよび句読点の代替コピーを制御することに、v4 プリンター ドライバーで書式の設定が改善されました。

**コピーの数**

これを指定する必要があるかどうか GPD ベースのプリンター ドライバーは、XPS-PCL6 にレンダリング フィルターを使用していて、ハードウェアのコピーをサポートしていません、  **\*HardwareCopies**コピー数の制御を実装するディレクティブ。 場合は、ディレクティブは ON に設定するか指定すると、このポリシーでは、フィルター ハードウェア コピー用の適切な PCL6 コマンドを複数のコピーを処理するために、デバイスに送信します。 それ以外の場合、このディレクティブが OFF に設定されている場合、フィルターすると、ソフトウェア コピーが生成されます。

**しない区切り文字の置換**

V3 プリンター ドライバーを使用して、履歴の実装のため、一部のデバイスにはピリオド (.) または PrintCapabilities で使用するにはハイフン (-) と PrintTicket の実装などの句読点が必要です。 既定の動作は、文字の置換が発生し続けることができます。 区切り文字の置換を構成するには、次に、ルート レベルの属性を指定します。

| ファイルの種類 | ディレクティブ                      | 必要な値 |
|-----------|--------------------------------|----------------|
| GPD       | \*NoPunctuationCharSubstitute でしょうか。 | True           |
| PPD       | \*MSPunctuationCharSubstitute  | True           |

 

## <a name="related-topics"></a>関連トピック
[V4 ドライバーの構成](v4-driver-configuration.md)  



