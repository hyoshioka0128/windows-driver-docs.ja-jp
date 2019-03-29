---
title: C28650
description: 0 が使用されている型エラーとして処理されませんが。
ms.assetid: faa24e4b-327c-42c7-92ee-33cd7b6ce5cb
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28650
ms.openlocfilehash: b8d17b0650bd63b7b7741b285c8e400290232077
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582342"
---
# <a name="c28650"></a>C28650


C28650 を警告します。対象の型です。 0 が使用されている処理されませんエラーとして。

状態値を返すなどです。TRUE は、失敗を示すステータス値を返すとは異なります。

などの特定のデータ型**NTSTATUS**と**HRESULT**を成功または失敗にこれらの型の値を分類するマクロが関連付けられています。 これらのマクロは、戻り値またはこれを確認する値の最上位ビットを確認します。 したがって、0 と 1 は両方として分類成功を示す値。

この警告を解決する適切な方法では、-1 などの一般的な値ではなく適切なエラー コードが返されます。

 

 





