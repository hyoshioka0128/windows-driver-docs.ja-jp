---
title: BindPrinter
description: IPrintTicketProvider BindPrinter メソッドは、印刷チケットのスキーマの特定のバージョンにプリンターまたは印刷キューをバインドします。
ms.assetid: 81f32a9a-417a-4851-972e-373112590e1c
keywords:
- BindPrinter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b6fcc1d89295dc760f0e9fd41795e83f8e0bebc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537020"
---
# <a name="bindprinter"></a>BindPrinter


[ **IPrintTicketProvider::BindPrinter** ](https://msdn.microsoft.com/library/windows/hardware/ff554354)メソッド プリンターまたは印刷キューを特定のバージョンの印刷チケットのスキーマにバインドします。 これにより、秘密の名前空間 Uri のセットをデバイスに関連付けるコア ドライバーです。

デバイスへのバインドは、特定のオブジェクトをキャッシュするプロバイダーを有効にし、使用は、そのデバイスの将来の印刷チケットまたはデバイスの機能のサービスを実行することを処理します。

[ **IPrintTicketProvider::BindPrinter** ](https://msdn.microsoft.com/library/windows/hardware/ff554354)メソッド PrintTicketProvider インスタンスごとに 1 回だけ呼び出されることが保証されます。

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
