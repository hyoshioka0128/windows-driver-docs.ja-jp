---
title: C28172
description: 関数は、PAGED_CODE または PAGED_CODE_LOCKED がページング セグメントに宣言されていない C28172 を警告します。
ms.assetid: c97bf9e8-583c-41ca-9c50-ac2af3dd5dc0
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28172
ms.openlocfilehash: 1569c1bc5f8e3cceed3c41a51fa3a2bb17f45de8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361472"
---
# <a name="c28172"></a>C28172


C28172 を警告します。関数がページングされた\_コードまたはページング\_コード\_ロック済みページ セグメントにするにはなりませんが、

ページを含む関数\_コードまたはページング\_コード\_を使用してページングされたメモリ内にロック済みのマクロが配置されていません**\#プラグマ アロケーション\_テキスト**または**\#プラグマ コード\_seg**します。 コード分析ツールでは、ページ セクション名の開始時にセクションではページング可能を推測します。 このエラーは、最初の中かっこに対応する行番号の位置報告 (**{**) 関数。

このエラーは、ページングの関数である場合に通常発生しますが、省略するか、間違っている、プラグマのいずれかがまたは非ページにページから、関数が変更された場合。 詳細については、次を参照してください。[警告 C28170](28170-pageable-code-macro-not-found.md)します。

 

 





