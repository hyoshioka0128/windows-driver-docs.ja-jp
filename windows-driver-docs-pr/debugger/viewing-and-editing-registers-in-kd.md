---
title: KD の表示と編集を登録します
description: KD では、表示および、r (レジスタ) コマンドを入力して、レジスタを編集することができます。 いくつかのオプションを使用するか、rm (登録マスク) コマンドを使用して、表示をカスタマイズできます。
ms.assetid: 42306338-6E11-4724-B62F-D1E0BDBA7F8D
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aef4589d8237dee7308f168cf4ff534850800013
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553735"
---
# <a name="viewing-and-editing-registers-in-kd"></a>KD の表示と編集を登録します


レジスタは、CPU 上にある小さな揮発性メモリ単位です。 多くのレジスタは、特定の用途専用し、その他のレジスタが使用するユーザー モード アプリケーションで利用できます。 X86 ベースおよび x64 ベース プロセッサでは、使用可能なレジスタのさまざまなコレクションがあります。 各プロセッサの詳細については、レジスタは、次を参照してください。[プロセッサ アーキテクチャ](processor-architecture.md)します。

KD の表示し、入力して、レジスタを編集、 [ **r (レジスタ)** ](r--registers-.md)コマンド。 画面をカスタマイズするには、いくつかのオプションを使用するかを使用して、 [ **rm (登録マスク)** ](rm--register-mask-.md)コマンド。

レジスタは、ターゲットを停止するたびとも自動的に表示されます。 使用してコードをステップ実行する場合、 [ **p (ステップ)** ](p--step-.md)または[ **t (トレース)** ](t--trace-.md)コマンド、レジスタのあらゆる段階で表示を表示します。 この表示を停止するには、使用、 **r**これらのコマンドを使用する場合します。

X86 ベースのプロセッサでは、上、 **r**オプションもフラグと呼ばれるいくつかの 1 ビット レジスタを制御します。 これらのフラグを変更するには、ときに、通常のレジスタを変更するよりも若干異なる構文を使用します。 詳細については、これらのフラグとこの構文の詳細については、次を参照してください。 [x86 フラグ](x86-architecture.md#x86-flags)します。

 

 




