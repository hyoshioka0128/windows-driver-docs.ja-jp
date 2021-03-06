---
title: IPrintCoreHelper インターフェイスの詳細
description: IPrintCoreHelper インターフェイスの詳細
ms.assetid: df736ca2-425e-4fc8-bdcb-bdbd5caa3e22
keywords:
- IPrintCoreHelper
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c130c1d466541f4ed047fb61b1998103a1aa218e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382045"
---
# <a name="details-of-the-iprintcorehelper-interface"></a>IPrintCoreHelper インターフェイスの詳細


**IPrintCoreHelper**インターフェイスは Pscript5 置換インターフェイスにほぼ基づいています。 ただし、これで 2 つの方法がある、 **IPrintCoreHelper**インターフェイスは、元の Pscript5 ヘルパー インターフェイスを基本的に異なります。

-   **IPrintCoreHelper**インターフェイスがありません、 **QuerySimulatedCapabilities**メソッド。 代わりに、 **IPrintCoreHelper**インターフェイスは、明確に定義されたと認識可能な方法で定期的機能とオプションの一覧にシミュレートされた機能をマップします。

-   **IPrintCoreHelper**インターフェイスを渡すため、呼び出し元がよく寄せられる、 [ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)の代わりに構造体、 [ **OEMUIOBJ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printoem/ns-printoem-_oemuiobj)構造体。

使用する場合、 **IPrintCoreHelper**インターフェイスまたはそこから継承するインターフェイスでは、次の点をする必要があります。

-   **IPrintCoreHelper**インターフェイスに使用される文字列、 **GetOption**または**SetOptions**メソッドは、GDL 文字列、その機能ではない、GPD 文字列とオプションで定義されている、 \#ifdef GDL ブロックは、ヘルパー インターフェイスのメソッドを使用できません。

-   場合、メソッド、 **IPrintCoreHelper**インターフェイス (およびそのサブインタ フェース) が OUT パラメーターと OUT パラメーターが、メソッドが呼び出されたときの値を保持するメソッドが失敗した場合。

-   メモリ モデル、 **IPrintCoreHelper**インターフェイスは、前の Pscript5 インターフェイスの若干異なります。 ヘルパー インターフェイスから渡されるパラメーターをクリーンアップする責任は呼び出し元と呼び出し元が渡されるバッファーを割り当てる必要はありません。 コア ドライバーでは、これらの種類のメモリ管理を処理します。

このセクションでは、次のトピックでは。

[IPrintCoreHelperUni インターフェイスの詳細](details-of-the-iprintcorehelperuni-interface.md)

[IPrintCoreHelperPS インターフェイスの詳細](details-of-the-iprintcorehelperps-interface.md)

 

 




