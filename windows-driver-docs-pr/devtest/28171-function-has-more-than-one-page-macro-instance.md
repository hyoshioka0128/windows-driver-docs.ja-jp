---
title: C28171
description: 関数には、警告 C28171 が PAGED_CODE または PAGED_CODE_LOCKED のインスタンスを 1 つ以上。
ms.assetid: 7a3740aa-53fc-4219-9606-edc0e9bd9879
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28171
ms.openlocfilehash: 6416fd9749c234decbbd002dc89babc0a042ca54
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553863"
---
# <a name="c28171"></a>C28171


C28171 を警告します。ページの 1 つ以上のインスタンスが関数には、\_コードまたはページング\_コード\_ロック

この警告は、ページの 1 つ以上のインスタンスがあることを示します\_コードまたはページング\_コード\_関数でマクロをロックします。 このエラーは、ページの 2 つ目またはそれ以降のインスタンスで報告\_コードまたはページング\_コード\_ロック済みのマクロ。

ページ セクションの関数は、ページの 1 つのインスタンスが必要\_コードまたはページング\_コード\_ロック済みのマクロとマクロは、最初の中かっこの間で関数の先頭に表示する必要があります (**{**) と、最初の条件付きステートメントと宣言の後にします。

これらのマクロを pREfast ドライバーの使用時に**\#プラグマ アロケーション\_テキスト**または**\#プラグマ コード\_seg**関数をページング可能なコードに移動するために使用セクション。 コード分析ツールでは、ページ セクション名の開始時にセクションではページング可能を推測します。 詳細については、次を参照してください。[警告 C28170](28170-pageable-code-macro-not-found.md)します。

 

 





