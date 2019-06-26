---
title: BindPrinter
description: IPrintTicketProvider BindPrinter メソッドは、印刷チケットのスキーマの特定のバージョンにプリンターまたは印刷キューをバインドします。
ms.assetid: 81f32a9a-417a-4851-972e-373112590e1c
keywords:
- BindPrinter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c6f6d41ea4f74e06d31f3343c1456186c027082
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384193"
---
# <a name="bindprinter"></a>BindPrinter


[ **IPrintTicketProvider::BindPrinter** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554354(v=vs.85))メソッド プリンターまたは印刷キューを特定のバージョンの印刷チケットのスキーマにバインドします。 これにより、秘密の名前空間 Uri のセットをデバイスに関連付けるコア ドライバーです。

デバイスへのバインドは、特定のオブジェクトをキャッシュするプロバイダーを有効にし、使用は、そのデバイスの将来の印刷チケットまたはデバイスの機能のサービスを実行することを処理します。

[ **IPrintTicketProvider::BindPrinter** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554354(v=vs.85))メソッド PrintTicketProvider インスタンスごとに 1 回だけ呼び出されることが保証されます。

次のサンプル コードは、メソッドの引数を示しています。

```cpp
STDMETHODIMP 
CPrintTicketProvider::
BindPrinter( THIS_ HANDLE    hPrinter,
                   INT       version,
                   PSHIMOPTS pOptions,
                   DWORD    *pDevModeFlags,
                   INT      *pcNamespaces,
                   BSTR    **ppNamespaces)
```
