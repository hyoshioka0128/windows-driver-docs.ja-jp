---
title: C28725
description: この SetUnhandledExceptionFilter ではなく C28725 使用ワトソンを警告します。
ms.assetid: 826B4BD2-226C-4986-86B3-E9DFD62DB225
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28725
ms.openlocfilehash: 467b727e7ffa20ea53e468898b5a302ecd5cd50d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323833"
---
# <a name="c28725"></a>C28725


C28725 を警告します。ワトソンを使用して、この SetUnhandledExceptionFilter ではなく

使用するアプリケーションでこの警告は報告、 [ **SetUnhandledExceptionFilter 関数**](https://msdn.microsoft.com/library/windows/desktop/ms680634)します。 プロセスの各スレッドの最上位の例外ハンドラーを置き換えるには、関数を使用できます。 既定では、システムが未処理の例外を渡します[Windows エラー報告](https://msdn.microsoft.com/library/windows/desktop/bb513641)(WER)。 セキュリティと利便性のためを参照してください。[を使用して WER](https://msdn.microsoft.com/library/windows/desktop/bb513616)します。

 

 





