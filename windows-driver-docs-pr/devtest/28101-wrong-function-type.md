---
title: C28101
description: 警告 C28101、ドライバーのモジュールが、現在の関数は、正しい種類の関数ではない推論します。
ms.assetid: 81a68dd6-ff9d-4cb2-9bd9-3a0f0d152230
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28101
ms.openlocfilehash: 52258c506cf53a14fb84f8e4b5a9941c00262b23
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364162"
---
# <a name="c28101"></a>C28101


C28101 を警告します。Drivers モジュールは、現在の関数は、正しい種類の関数ではない推定します。

コード分析ツールは、コールバック関数など、特定の種類の関数がいます。 これは、専用メッセーです。 エラーは示されません。

このメッセージは、コード分析ツールがその関数の型に固有のルールを適用することを示します。 この推定が間違っている場合は、コード分析ツール、偽陽性の警告が生成されますが、それらの警告は無視してかまいません。 詳細については、次を参照してください。 [C と C++ コードの欠陥を削減するのを使用して注釈](https://go.microsoft.com/fwlink/p/?linkid=227826)します。

*関数シグネチャ*(引数と結果型) が可能であれば関数を識別するために使用します。 いくつかの標準のドライバー ルーチンなど[**キャンセル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)と[ **StartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)名前をチェックして、同じシグネチャがあることその関数に対して従来の名前と一致します。 従来の名前には、その他の機能をチェックする可能性があります。

冗長になる場合、この警告を非表示に、関数の特定の関数型を明示的に宣言することができます。 この方法で検出された関数は、コールバック関数では通常します。 適切なアクションは宣言関数の typedef を使用することです。 詳細については、次を参照してください。[を使用して関数の役割の型の宣言](using-function-role-type-declarations.md)します。

 

 





