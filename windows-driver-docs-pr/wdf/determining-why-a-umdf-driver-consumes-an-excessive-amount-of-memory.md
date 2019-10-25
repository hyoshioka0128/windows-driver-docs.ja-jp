---
title: UMDF ドライバーが過剰なメモリを消費する理由
description: Wudfext .dll を使用して、UMDF version 1 ドライバーが大量のメモリを消費する理由を確認する方法について説明します。
ms.assetid: 01316c4e-24e8-467c-af52-900b3fe042db
keywords:
- デバッグシナリオ WDK UMDF、UMDF ドライバーが過剰なメモリを消費する
- UMDF WDK、デバッグシナリオ、UMDF ドライバーが過剰なメモリを消費する
- UMDF WDK、UMDF ドライバーは過剰なメモリを消費する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0955d276d1cbd51ebec7e8bdd38ea186ba061190
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840387"
---
# <a name="determining-why-a-umdf-driver-consumes-an-excessive-amount-of-memory"></a>UMDF ドライバーが大量にメモリを消費する理由の特定

[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

このトピックでは、Wudfext デバッガー拡張機能をユーザーモードドライバーフレームワーク (UMDF) バージョン1ドライバーと組み合わせて使用して、UMDF ドライバーが大量のメモリを消費する原因を特定する方法について説明します。

UMDF バージョン2以降では、代わりに、Wdfkd デバッガー拡張機能を使用する必要があります。 詳細については、「 [Windows Driver Framework Extensions (Wdfkd .dll)](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)」を参照してください。

メモリ使用量を調査するには、次の手順を使用します。

1.  オブジェクトツリー内の未処理のオブジェクトを表示するには、 **! wudfext. wudfext**の UMDF デバッガー拡張機能を使用します。

    **! Wudfext. wudfext**拡張機能には、親と子のリレーションシップを含む WDF オブジェクトに関する情報が表示されます。 *Flags*パラメーターのビット0を 1 (0x01) に設定すると、 **! wudfext. wudfext**は、渡されたオブジェクトをルートとするオブジェクトツリーの再帰ダンプを実行します。 完全なオブジェクトツリーを表示するには、次のコマンド例を使用します。

    **! wudfext. wudfext &lt;IWDFDriver\*&gt; 1**

2.  未解決のオブジェクトが予想よりも多いかどうかを確認します。

    ドライバーが最終的にこれらのオブジェクトをリークする可能性があります (WDF オブジェクトのリークの詳細については、「[ドライバーがフレームワークオブジェクトをリークするか](determining-if-a-driver-leaks-framework-objects.md)どうかを判断する」を参照してください)。

    これらのオブジェクトはオブジェクトツリーに存在する可能性があるため、最終的に解放されます。 ただし、これらは不必要に蓄積されています。 次のオブジェクトが必要になる場合があります。

    -   親オブジェクトの修正。
    -   [**Iwdfobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)を使用した明示的な削除::D eletewdfobject メソッド。

 

 





