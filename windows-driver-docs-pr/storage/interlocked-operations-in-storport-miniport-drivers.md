---
title: Storport ミニポート ドライバーのインタロックされた操作
description: Windows アプリケーションで使用できるインタロックされた関数の多くは、Storport ミニポートドライバーでの使用に適しています。
ms.assetid: F3868AF4-545F-4B8E-8655-5AAD888C4B40
ms.date: 06/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: f77a33df8fe404a160b5e330f6411a2fcfa400a4
ms.sourcegitcommit: b795323cafe6b38918a33d3ecdf6b1a46215693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2019
ms.locfileid: "70839648"
---
# <a name="interlocked-operations-in-storport-miniport-drivers"></a>Storport ミニポート ドライバーのインタロックされた操作

アプリケーションは、プラットフォームソフトウェア開発キット (SDK) のインタロックされた関数を使用して、複数のスレッドで共有されている変数へのアクセスを同期する必要があります。 Windows アプリケーションで使用できるインタロックされた関数の多くは、Storport ミニポートドライバーでの使用に適しています。 これらの関数のほとんどは[コンパイラの組み込み関数](https://docs.microsoft.com/cpp/intrinsics/compiler-intrinsics?view=vs-2019)として実装されており、保護された値への変更の同期に適しています。
関数は、論理、代入、比較、および組み込み算術の各操作に対して定義されます。

インタロック操作の詳細については、「[インタロック変数アクセス](https://docs.microsoft.com/windows/desktop/Sync/interlocked-variable-access)」を参照してください。

**メモ** **インタロックされた *Xxx*** 関数は、storport で *、または*32 ビット (x86) ドライバーの場合は*storport*で宣言されます。
