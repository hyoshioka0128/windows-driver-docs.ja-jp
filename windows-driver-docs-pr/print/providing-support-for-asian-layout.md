---
title: レイアウトのアジア言語のサポートを提供します。
description: レイアウトのアジア言語のサポートを提供します。
ms.assetid: 38c7dfca-ce30-4967-84a4-e2f40bba8c57
keywords:
- プリント プロセッサ WDK、アジアの言語
- WDK のアジア言語を印刷します。
- WDK の小冊子を印刷します。
- N アップ印刷 WDK
- WDK の印刷の向きを反転します。
- WDK にアラビア語の印刷のサポート
- WDK に日本語の印刷のサポート
- WDK にウルドゥ語の印刷のサポート
- WDK 考慮事項
- WDK のアジア言語の印刷
- WDK の言語を印刷します。
- 右から左に読む言語 WDk を印刷します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89c49b95b8c7a45bbde4b33e9b0b85387d3bb0e6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527288"
---
# <a name="providing-support-for-asian-layout"></a>レイアウトのアジア言語のサポートを提供します。


Microsoft Windows では、右から次の機能がアラビア語、日本語、およびウルドゥ語などの左に読むプロセッサ サポートのアジア言語を印刷します。

-   **N-up 方向**:1 枚に複数のページを印刷する場合、ユーザーは、シート上、右から左の順序でページを印刷できます。

-   **小冊子 Edge**:シートを折りたたむし、並列でページのレイアウトが、小冊子を印刷する場合、ユーザーは、右から左に小冊子のページを注文できます。 次の図は、小冊子を使用して、小冊子のページ レイアウトは\_EDGE\_適切なフラグ![。小冊子を使用して、小冊子のページ レイアウトを示す図\-edge\-右フラグ](images/asian-booklet.png)

アジア言語のレイアウトをサポートするために、ドライバーの n-up 方向および小冊子のエッジを変更するためのフラグは、Windows Vista で利用できます。 これらの値を設定する方法の詳細については、次を参照してください[ **DrvQueryJobAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff548581)と[**属性\_情報\_4** ](https://msdn.microsoft.com/library/windows/hardware/ff545096).

 

 




