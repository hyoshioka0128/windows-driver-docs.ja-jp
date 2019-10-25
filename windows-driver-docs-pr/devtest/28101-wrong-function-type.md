---
title: C28101
description: Warning C28101 Drivers モジュールは、現在の関数が正しい型の関数ではないと推論しました。
ms.assetid: 81a68dd6-ff9d-4cb2-9bd9-3a0f0d152230
keywords:
- ドライバーの WDK PREfast の一覧に警告が表示される
- ドライバーの WDK PREfast の一覧にエラーが表示される
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28101
ms.openlocfilehash: 33d8f9fdf3bf4c2bca614e86396c650a017ae5c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840319"
---
# <a name="c28101"></a>C28101


warning C28101: Drivers モジュールは、現在の関数が正しい型の関数ではないと推論しました

コード分析ツールにより、関数がコールバック関数などの特定の型であることが検出されました。 このメッセージは情報提供だけを目的としています。 エラーを示すものではありません。

このメッセージは、コード分析ツールが、その関数の種類に固有のルールを適用していることを示します。 この推論が間違っている場合は、コード分析ツールによって偽陽性の警告が生成されますが、これらの警告は無視しても安全です。 詳細については、「[注釈を使用しC++て C/コードの欠陥を減らす](https://go.microsoft.com/fwlink/p/?linkid=227826)」を参照してください。

関数*シグネチャ*(引数と結果型) は、可能な限り関数を識別するために使用されます。 [**Cancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)や[**StartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)などの一部の標準ドライバールーチンは同じシグネチャを持っているため、名前がその関数の従来の名前と一致するかどうかが確認されます。 従来の名前については、他の関数がチェックされる場合があります。

冗長である場合にこの警告を抑制するには、関数を特定の関数型として明示的に宣言します。 この方法で検出された関数は、通常、コールバック関数です。 適切なアクションとして、関数 typedef を使用して宣言します。 詳細については、「[関数ロール型宣言の使用](using-function-role-type-declarations.md)」を参照してください。

 

 





