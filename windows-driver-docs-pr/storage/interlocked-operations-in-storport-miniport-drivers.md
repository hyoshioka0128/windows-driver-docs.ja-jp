---
title: Storport ミニポート ドライバーのインタロックされた操作
description: Windows アプリケーションで使用できるインタロックされた関数の多くは、Storport ミニポートドライバーでの使用に適しています。
ms.assetid: F3868AF4-545F-4B8E-8655-5AAD888C4B40
ms.date: 06/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6e9b3f2d61225419ddd8bd58c4892b0336db5188
ms.sourcegitcommit: 238308264c1ee2c74ec0c8c303258dc00c79b902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2019
ms.locfileid: "70063907"
---
# <a name="interlocked-operations-in-storport-miniport-drivers"></a>Storport ミニポート ドライバーのインタロックされた操作

アプリケーションは、プラットフォームソフトウェア開発キット (SDK) のインタロックされた関数を使用して、複数のスレッドで共有されている変数へのアクセスを同期する必要があります。 Windows アプリケーションで使用できるインタロックされた関数の多くは、Storport ミニポートドライバーでの使用に適しています。 これらの関数のほとんどは[コンパイラの組み込み関数](https://docs.microsoft.com/cpp/intrinsics/compiler-intrinsics?view=vs-2019)として実装されており、保護された値への変更の同期に適しています。
関数は、論理、代入、比較、および組み込み算術の各操作に対して定義されます。

インタロック操作の詳細については、「[インタロック変数アクセス](https://docs.microsoft.com/windows/desktop/Sync/interlocked-variable-access)」を参照してください。

**注:**   インタロックされた *** Xxx***関数は、32ビット (x86) ドライバーの場合は、 *storport*で宣言します。