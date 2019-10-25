---
title: IPrintCoreHelper インターフェイスの詳細
description: IPrintCoreHelper インターフェイスの詳細
ms.assetid: df736ca2-425e-4fc8-bdcb-bdbd5caa3e22
keywords:
- IPrintCoreHelper
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85e5ab345d54c806c29a016bfb1a6e41c4c7a7f2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829020"
---
# <a name="details-of-the-iprintcorehelper-interface"></a>IPrintCoreHelper インターフェイスの詳細


**Iprintcorehelper**インターフェイスは、Pscript5 UI の置換インターフェイスにほぼ基づいています。 ただし、 **Iprintcorehelper**インターフェイスが元の Pscript5 ヘルパーインターフェイスと基本的に異なる2つの方法があります。

-   **Iprintcorehelper**インターフェイスには、 **QuerySimulatedCapabilities**メソッドがありません。 代わりに、 **Iprintcorehelper**インターフェイスは、シミュレートされた機能を明確に定義された、認識可能な方法で、特徴とオプションの通常の一覧にマップします。

-   **Iprintcorehelper**インターフェイスでは、呼び出し元は、 [**oemuiobj**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ns-printoem-_oemuiobj)構造体ではなく、 [**devmodew**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)構造体で渡すように要求されます。

**Iprintcorehelper**インターフェイスまたはそれを継承するインターフェイスを使用する場合は、次の点を考慮する必要があります。

-   **Iprintcorehelper**インターフェイスでは、 **GetOption**メソッドまたは**SetOptions**メソッドに使用される文字列は、GDL 文字列ではなく GPD 文字列であるため、\#ifdef gdl ブロックで定義されている機能とオプションは使用できません。ヘルパーインターフェイスメソッド。

-   **Iprintcorehelper**インターフェイス (およびそのサブインターフェイス) のメソッドに OUT パラメーターがあり、メソッドが失敗した場合、out パラメーターは、メソッドが呼び出されたときの値を保持します。

-   **Iprintcorehelper**インターフェイスのメモリモデルは、前の Pscript5 インターフェイスとは少し異なります。 呼び出し元は、ヘルパーインターフェイスから返されたパラメーターをクリーンアップする責任を負いません。また、呼び出し元は、渡されるバッファーを割り当てる必要はありません。 コアドライバーは、これらの種類のメモリ管理を処理します。

ここでは、次のトピックについて説明します。

[Iprintcoreの Peruni インターフェイスの詳細](details-of-the-iprintcorehelperuni-interface.md)

[Iprintcoreの Perps インターフェイスの詳細](details-of-the-iprintcorehelperps-interface.md)

 

 




