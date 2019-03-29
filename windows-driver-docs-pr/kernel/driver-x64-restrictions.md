---
title: ドライバーの x64 に関する制限
description: ドライバーの x64 に関する制限
ms.assetid: 717ca559-93aa-48d6-8347-bfdf223f1aa4
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c16389945a5b6b96fcc2b87c7cf73b92ce730289
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578972"
---
# <a name="driver-x64-restrictions"></a>ドライバーの x64 に関する制限


X64 ベースのシステムのカーネル コードと特定のカーネル データ構造が変更から保護されます。 このようなコードやデータを変更しようとする任意のドライバーとシステムのバグ チェックが、(CRITICAL で\_構造\_破損バグ チェック)。

X64 ベース システム用のドライバーには、このバグ チェックがトリガーされる操作を回避する必要があります。 具体的には、ドライバーは許可されません。

-   実行時にカーネル コードを変更しようとしてください。

-   実装し、独自のスタックを使用します。

-   割り込みディスパッチ テーブル (IDT) またはグローバルの記述子テーブル (GDT) など、ハードウェアのディスパッチ テーブルを変更します。

-   ドキュメントに未記載のカーネル データ構造を変更します。

上述の操作がトリガーされない場合でも、バグを確認 x86 ベースまたは Itanium ベース システムでは、ドライバーは任意のプラットフォームでこれらの操作のいずれかを実行しない必要があります。 これらの操作が機能しない将来のバージョンの Microsoft Windows オペレーティング システム。

カーネル コードとデータ構造を変更する方法の詳細については、次を参照してください。、 [x64 ベース システム用の修正プログラムの適用ポリシー](https://go.microsoft.com/fwlink/p/?linkid=50719)ホワイト ペーパー、 [64 ビットの修正プログラムの適用に関する FAQ](https://go.microsoft.com/fwlink/p/?linkid=69534)します。

64 ビット コンパイラを使用したプログラミングに関する概要については、次を参照してください。 [64 ビットの Visual c を使用したプログラミング](https://go.microsoft.com/fwlink/p/?linkid=165521)します。

 

 




