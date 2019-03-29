---
title: TCP/IP プリンターのインストール
description: TCP/IP プリンターのインストール
ms.assetid: 15339cce-69aa-480d-bfee-11ea509ff5d4
keywords:
- WDK の TCP/IP プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b7bce0ae75003b7bc7648497afb8308a8871a0a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578568"
---
# <a name="installing-tcpip-printers"></a>TCP/IP プリンターのインストール


TCP/IP を使用するネットワーク上のプリンターでは、TCP ポート モニターをインストールし、プリンターを構成するの機能を利用できます。

-   **自動検出**:サブネット上のすべての TCP/IP プリンターが自動的に検出し、インストールされています。

-   **自動選択**:プリンター ドライバーは、TCP/IP プリンターがインストールされて、新しいプリンター ポート モニター管理情報ベース (MIB) または Tcpmon.ini のいずれかから取得された情報に基づいて自動的に選択できます。

これらの機能は、Windows Vista で導入されました。

### <a name="port-monitor-mibs"></a>ポート モニター (mib)

プリンター拡張の MIB 仕様では、ネットワーク カード パラメーターの追加の容量を提供します。 この拡張機能では、Windows Vista より前に、のバージョンの Windows で Tcpmon.ini のみに格納されていたプリンター情報のカスタマイズができます。

この拡張の MIB を使用すると、Tcpmon.ini を変更することがなくプリンター情報に更新プログラムを管理できます。 拡張の MIB が実装されていない場合、TCP ポート モニターは Tcpmon.ini を使用してに戻ります。

拡張の MIB 仕様の詳細については、次を参照してください。、[プリンター ポート モニター MIB v1.0](https://go.microsoft.com/fwlink/p/?linkid=526286)プリンター Working Group のドキュメント。

 

 




