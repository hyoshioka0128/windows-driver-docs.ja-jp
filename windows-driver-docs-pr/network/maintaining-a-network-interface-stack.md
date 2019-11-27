---
title: ネットワーク インターフェイス スタックの保守
description: ネットワーク インターフェイス スタックの保守
ms.assetid: c51a2e5b-28ad-4e86-8b37-1491f85a17bb
keywords:
- NDIS ネットワークインターフェイス WDK、スタックメンテナンス
- ネットワークインターフェイス WDK、スタックメンテナンス
- スタック WDK ネットワーク
- インターフェイススタックテーブル WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cc8954262f47fb7242b76cc1c8220b103220484
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844133"
---
# <a name="maintaining-a-network-interface-stack"></a>ネットワーク インターフェイス スタックの保守





NDIS には、インターフェイススタックテーブル (RFC 2863 の*Ifstacktable* ) を維持するサービスが用意されています。 Ndis は ndis ミニポートアダプター (NDIS 5) のスタックテーブルを保持します。*x*フィルター中間ドライバーおよび NDIS フィルターモジュール。 また、NDIS は、NDIS ドライバーがこのテーブル内のエントリを追加および削除できるようにするサービスも提供します。 MUX 中間ドライバーの場合、NDIS は、仮想ミニポートインターフェイスとプロトコル下位インターフェイスの間の関係にアクセスできません。 したがって、NDIS 6.0 MUX 中間ドライバーでは、これらの内部インターフェイス関係を指定する必要があります。

2つのインターフェイス間のスタック関係を定義するために、すべての NDIS ドライバーは、NdisIfAddIfStackEntry 関数に*Higher$ erifindex* *パラメーターと* [](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifaddifstackentry)パラメーターを渡すことができます。 これらのパラメーターでは、ネットワークインターフェイススタックの上位にある1つのネットワークインターフェイスと、スタックの下位にある1つのネットワークインターフェイスを指定します。

別のインターフェイスに関連付けられているインターフェイスに関するスタック順情報 (たとえば、NDIS から参照できない MUX 中間ドライバーの内部バインドなど) があるドライバーは、 **NdisIfAddIfStackEntry**を呼び出してインターフェイススタックテーブルを設定します. スタックエントリが正常に作成された場合、この関数は NDIS\_STATUS\_SUCCESS を返します。 通常、またはを所有するコンポーネントは、上位層インターフェイスのインターフェイスプロバイダーである ( *Higher$ Erifindex*によって識別されます) **NdisIfAddIfStackEntry**を呼び出します。

スタックテーブルのエントリを削除するために、ドライバーは、 [**NdisIfDeleteIfStackEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifdeleteifstackentry)関数に*Higher$ erifindex* *パラメーターと*より高速パラメーターを渡します。

インターフェイススタックを維持する例については、「MUX 6.0 サンプルドライバー」を参照してください。

 

 





