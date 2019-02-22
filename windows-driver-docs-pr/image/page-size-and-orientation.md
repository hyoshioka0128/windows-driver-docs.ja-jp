---
title: ページ サイズと向き
description: ページ サイズと向き
ms.assetid: f744a00c-8614-4488-9a29-d193a0c4268f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb14620afd918ce89f50fc0c9843f8fa92fe2d08
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538826"
---
# <a name="page-size-and-orientation"></a>ページ サイズと向き


ページ サイズと向きのスキャナーの設定が相互にします。 両方は、スキャンするページのサイズを決定します。

たとえば、ページ サイズと範囲の値 WIA で使用される\_PROP\_一覧は、WIA の有効な設定に依存\_IP\_ORIENTATION プロパティ。 そのため、デバイスが、WIA 横向きのドキュメントをスキャンできないかどうか\_ページ\_A4 設定、WIA\_ページ\_A4 が、wia の有効な値の一覧に表示されない\_IP\_ページ\_SIZE プロパティと WIA\_IP\_LANSCAPE に設定されます。

値、 [ **WIA\_IP\_向き**](https://msdn.microsoft.com/library/windows/hardware/ff552625)プロパティは、現在選択されているページの向きを決定します。 [ **WIA\_IP\_ページ\_高さ**](https://msdn.microsoft.com/library/windows/hardware/ff552632)と[ **WIA\_IP\_ページ\_幅**](https://msdn.microsoft.com/library/windows/hardware/ff552636)プロパティ ページのサイズをインチの部分の 1/1000 でのレポート (. 001)。 これらの高さと幅のプロパティの値に相当する値を含める必要があります[ **WIA\_IP\_XEXTENT** ](https://msdn.microsoft.com/library/windows/hardware/ff552661)と[ **WIA\_IP\_YEXTENT**](https://msdn.microsoft.com/library/windows/hardware/ff552669)ページの寸法をピクセル単位で提供します。

ページ サイズと向きを操作の詳細については、次のトピックを参照してください。

[サポートされているスキャナーの用紙サイズ](supported-scanner-paper-sizes.md)

[カスタム プロパティと自動ページ サイズ](custom-and-auto-page-sizes.md)

[ページの向き](page-orientation.md)

[スキャナーのページ サイズと向きのコード例](page-size-and-orientation-code-examples.md)

 

 




