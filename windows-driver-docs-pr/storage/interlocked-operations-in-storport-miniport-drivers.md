---
title: Storport ミニポート ドライバーのインタロックされた操作
description: Windows アプリケーションで使用できるインター ロックされた関数の多くは、Storport ミニポート ドライバーでの使用に適しています。
ms.assetid: F3868AF4-545F-4B8E-8655-5AAD888C4B40
ms.date: 06/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: e9b52cbbace16d260ff34fb72546d56fd0f54563
ms.sourcegitcommit: 91b989fc3256267fab89c36b1fa54ff039dcc687
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "67148523"
---
# <a name="interlocked-operations-in-storport-miniport-drivers"></a>Storport ミニポート ドライバーのインタロックされた操作

アプリケーションでは、そのためにはプラットフォーム ソフトウェア開発キット (SDK) interlocked 関数を使用して、複数のスレッドによって共有される変数へのアクセスを同期する必要があります。 Windows アプリケーションで使用できるインター ロックされた関数の多くは、Storport ミニポート ドライバーでの使用に適しています。 これらの関数のほとんどとして実装されて[コンパイラ組み込み関数](https://docs.microsoft.com/cpp/intrinsics/compiler-intrinsics?view=vs-2019)は保護されている値の変更を同期するために適しています。
関数は、論理、代入、比較、および算術演算に対して定義されます。

インタロックされた操作の詳細については、次を参照してください。[変数アクセスのインタロックされた](https://docs.microsoft.com/en-us/windows/desktop/Sync/interlocked-variable-access)します。

**注**  、 **Interlocked * Xxx*** 関数で宣言されます*miniport.h*または 32 ビット (x86) ドライバーで*storport.h*します。