---
title: WDM の下端の実装のヒントと要件
description: WDM の下端の実装のヒントと要件
ms.assetid: 760c62ec-eeca-4b62-97ec-7cda5ee353a8
keywords:
- NDIS WDM ミニポート ドライバー WDK ネットワー キング、実装に関するヒント
- 下端の NDIS ミニポート ドライバー WDK ネットワー キング、ドライバーの実装
- WDM 低い edge WDK ネットワー キング、ドライバーの実装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ab16f15313e8369134d73c910ddb33a11daf261
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362562"
---
# <a name="implementation-tips-and-requirements-for-wdm-lower-edge"></a>WDM の下端の実装のヒントと要件





このトピックでは、ヒントや、NDIS WDM ミニポート ドライバーを実装するための要件について説明します。 NDIS WDM のミニポート ドライバーでは、NDIS と NDIS 以外の両方の関数を呼び出すことができます。 たとえば、WDM カーネル モードのサポート ルーチンと特定のバス ドライバー インターフェイスの関数これら NDIS 以外の機能があります。

NDIS WDM のミニポート ドライバーを実装する場合は、次に留意してください。

-   構築、NDIS WDM ミニポート ドライバーが必要です、NDIS\_Ndis.h ヘッダー ファイルが含まれる前に、WDM フラグが定義されています。 NDIS を定義する\_WDM フラグに確実に Ndis.h は、適切な WDM ヘッダー ファイルを自動的に含めます。 NDIS\_するか、ミニポート ドライバーのソース コードの先頭に埋め込まれたまたは、ミニポート ドライバーのソース ファイルで設定する必要があります WDM フラグ。 NDIS WDM のミニポート ドライバーには、カーネル モードのルーチンを呼び出すに WDM ヘッダー ファイルが必要です[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)と[ **IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257).

-   特定のバス ドライバー インターフェイスの関数呼び出しでは、バス ドライバーのヘッダー ファイルが必要です。

-   互換性がない可能性があるため、同じソース ファイル内の NDIS および NDIS 以外のヘッダーを含むはお勧めしません。 別のソース ファイルは、NDIS 関数を呼び出すコードと非 NDIS 関数を呼び出すコードを作成する必要があります。

-   NDIS WDM のミニポート ドライバーでは、割り当て、NDIS WDM ミニポート ドライバーを割り当てるし、次のシナリオのいずれかでリソースを解放しない限り、リソースを解放する適切な NDIS 関数を呼び出す必要があります。

    -   リソース、メモリ リソースでは通常、NDIS WDM ミニポート ドライバーが割り当てられるし、バス ドライバー インターフェイスなどの非 NDIS エンティティによって後でリリース
    -   通常、メモリ リソースのリソースでは、NDIS 以外のエンティティによって割り当てられていますされ、NDIS WDM ミニポート ドライバーによって後で解放されます。

    上記のシナリオでは、NDIS WDM ミニポート ドライバーは、割り当て/NDIS 以外のエンティティのリソースを解放するために適切な WDM ルーチンを呼び出す必要があります。

 

 





