---
title: TCP/IP プリンターのインストール
description: TCP/IP プリンターのインストール
ms.assetid: 15339cce-69aa-480d-bfee-11ea509ff5d4
keywords:
- TCP/IP WDK プリンター
ms.date: 06/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: b990999a2a9ab0c47a3926cad06c45e5fdf26425
ms.sourcegitcommit: 581fb777a2376854ca12e767d366e2cb79724b73
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2020
ms.locfileid: "84461833"
---
# <a name="installing-tcpip-printers"></a>TCP/IP プリンターのインストール

TCP/IP を使用するネットワークプリンターでは、TCP ポートモニターの機能を利用して、プリンターをインストールして構成できます。

- **自動検出**: サブネット上のすべての tcp/ip プリンターが自動的に検出され、インストールされます。

- **自動選択**: プリンタードライバーは、新しいプリンターポートモニター管理情報ベース (MIB) または tcpmon .ini から取得された情報に基づいて、tcp/ip プリンターをインストールするときに自動的に選択できます。

これらの機能は、Windows Vista で導入されました。

## <a name="port-monitor-mibs"></a>ポートモニターの Mib

プリンターの MIB 仕様の拡張により、ネットワークカードのパラメーターに追加の容量が提供されます。 この拡張機能により、windows Vista より前の Windows バージョンでは、Tcpmon にのみ保存されていたプリンター情報をカスタマイズできます。

この拡張 MIB を使用することにより、Tcpmon .ini を変更することなく、プリンター情報の更新を管理できます。 拡張 MIB が実装されていない場合、TCP ポートモニターは Tcpmon を使用するように戻ります。

拡張 MIB 仕様の詳細については、[プリンタポートモニタ MIB](https://go.microsoft.com/fwlink/p/?linkid=526286) V1.0 プリンタワーキンググループドキュメントを参照してください。
