---
title: データのインデックス
description: データのインデックス
ms.assetid: 84577544-515a-4fdc-86e5-518182c6c461
keywords:
- WDK を非表示にデータをインデックスします。
- インデックス データの WDK を非表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d1fdb684c05c16f07998c25814f401bdd09d8ad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538392"
---
# <a name="data-indices"></a>データのインデックス





HID パーサーを割り当てます、*データ インデックス*を最上位のコレクションで説明されている各使用法を一意に識別[機能の配列をボタン](button-capability-arrays.md)と[機能配列値](value-capability-arrays.md). 概念的には、データのインデックスは、ユーザー モード アプリケーションまたはカーネル モード ドライバーは、レポート内の個々 のコントロールのデータへのアクセスに使用できる配列の 0 から始まるインデックスです。 パーサーは、各最上位のコレクションでサポートされているレポートの種類ごとにデータのインデックスの一意のセットを割り当てます。

機能の構造体は、次のように、使用法とデータのインデックスを相互参照します。

-   各機能の構造の使用方法を説明するがその**NotRange.Usage**メンバーのセットを使用状況を特定し、その**NotRange.DataIndex** usage に設定するメンバーのデータのインデックスに対応します。

-   使用状況の範囲を説明する各機能の構造がその**Range.UsageMin**と**Range.UsageMax**使用状況の範囲を識別するためにメンバーを設定し、その**Range.DataIndexMin**と**Range.DataIndexMax**使用状況の範囲を識別するためにメンバー セットのデータ インデックスの範囲に対応します。 (*データ範囲のインデックス*データのインデックスの連続するシーケンスと、データのインデックスの範囲内のデータのインデックスの数が対応する使用状況の範囲の使用法の値に等しいを指定します)。

データのインデックスを使用する方法の詳細については、次を参照してください。[設定コントロールのデータをデータのインデックスと抽出](extracting-and-setting-control-data-by-data-indices.md)します。

 

 




