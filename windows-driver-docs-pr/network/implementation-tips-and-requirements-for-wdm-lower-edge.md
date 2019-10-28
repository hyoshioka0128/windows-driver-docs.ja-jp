---
title: WDM の下端の実装のヒントと要件
description: WDM の下端の実装のヒントと要件
ms.assetid: 760c62ec-eeca-4b62-97ec-7cda5ee353a8
keywords:
- NDIS-WDM ミニポートドライバー WDK ネットワーク、実装ヒント
- NDIS ミニポートドライバー WDK ネットワーク、driver 実装のエッジ下部
- WDM 低エッジ WDK ネットワーク、driver 実装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3334b8edb748f594f7df04b028c4b5e72000d37e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843444"
---
# <a name="implementation-tips-and-requirements-for-wdm-lower-edge"></a>WDM の下端の実装のヒントと要件





このトピックでは、NDIS-WDM ミニポートドライバーを実装するためのヒントと要件について説明します。 NDIS-WDM ミニポートドライバーは、ndis と非 NDIS の両方の機能を呼び出すことができます。 これらの非 NDIS 関数には、たとえば、WDM-カーネルモードのサポートルーチンと、特定のバスドライバーインターフェイスの関数が含まれます。

NDIS-WDM ミニポートドライバーを実装する場合は、次の点に注意してください。

-   Ndis-WDM ミニポートドライバーをビルドするには、ndis .h ヘッダーファイルが含まれる前に NDIS\_WDM フラグが定義されている必要があります。 NDIS\_WDM フラグを定義すると、適切な WDM ヘッダーファイルが確実に Ndis .h に自動的に含まれるようになります。 NDIS\_WDM フラグは、ミニポートドライバーのソースコードの先頭に埋め込まれているか、ミニポートドライバーのソースファイルに設定されている必要があります。 NDIS-WDM ミニポートドライバーでは、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)や[**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)などのカーネルモードルーチンを呼び出すために、wdm ヘッダーファイルが必要です。

-   特定のバスドライバーインターフェイスの関数呼び出しには、そのバスドライバーのヘッダーファイルが必要です。

-   同じソースファイルに NDIS ヘッダーと非 NDIS ヘッダーを含めることは、互換性がない可能性があるため、推奨されません。 つまり、ndis 関数を呼び出すコードと、非 NDIS 関数を呼び出すコードには、個別のソースファイルを作成する必要があります。

-   Ndis-wdm ミニポートドライバーは、次のいずれかのシナリオでリソースの割り当てと解放を行う場合を除き、リソースの割り当てと解放を行うために適切な NDIS 関数を呼び出す必要があります。

    -   リソース (通常はメモリリソース) は、NDIS-WDM ミニポートドライバーによって割り当てられ、後でバスドライバーインターフェイスなどの非 NDIS エンティティによって解放されます。
    -   リソース (通常はメモリリソース) は、NDIS 以外のエンティティによって割り当てられ、後で NDIS-WDM ミニポートドライバーによって解放されます。

    前のシナリオでは、NDIS-WDM ミニポートドライバーは、適切な WDM ルーチンを呼び出して、非 NDIS エンティティのリソースを割り当てたり解放したりする必要があります。

 

 





