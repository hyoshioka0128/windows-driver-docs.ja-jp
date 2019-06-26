---
title: C28725
description: この SetUnhandledExceptionFilter ではなく C28725 使用ワトソンを警告します。
ms.assetid: 826B4BD2-226C-4986-86B3-E9DFD62DB225
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28725
ms.openlocfilehash: 33f105222db65259d2bcf62b82011f8bd54f8996
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371717"
---
# <a name="c28725"></a>C28725


C28725 を警告します。ワトソンを使用して、この SetUnhandledExceptionFilter ではなく

使用するアプリケーションでこの警告は報告、 [ **SetUnhandledExceptionFilter 関数**](https://docs.microsoft.com/windows/desktop/api/errhandlingapi/nf-errhandlingapi-setunhandledexceptionfilter)します。 プロセスの各スレッドの最上位の例外ハンドラーを置き換えるには、関数を使用できます。 既定では、システムが未処理の例外を渡します[Windows エラー報告](https://docs.microsoft.com/windows/desktop/wer/windows-error-reporting)(WER)。 セキュリティと利便性のためを参照してください。[を使用して WER](https://docs.microsoft.com/windows/desktop/wer/using-wer)します。

 

 





