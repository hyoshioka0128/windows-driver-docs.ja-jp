---
title: ポート構成情報の格納
description: ポート構成情報の格納
ms.assetid: b1c83729-d7d2-4920-9402-4e00baa12633
keywords:
- ポート管理 WDK 印刷、構成情報の保存
- レジストリ WDK 印刷
- 印刷スプーラレジストリ情報 WDK 印刷モニター
- 印刷ポートの構成情報の保存
- スプーラレジストリ情報 WDK 印刷モニター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9aae43356ab04ba29c30acbca322ca4570fb8f2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844411"
---
# <a name="storing-port-configuration-information"></a>ポート構成情報の格納





Windows 2000 以降の印刷スプーラは、クラスター化または非クラスター化サーバー環境で動作できます。 サーバークラスターでスプーラが動作している場合は、印刷モニターの構成情報をクラスターレジストリに保存する必要があります。 一方、スプーラが単一の非クラスター化サーバーシステムで動作している場合は、印刷モニターの構成情報をサーバーのローカルレジストリに保存する必要があります。

印刷スプーラでは、印刷モニターで使用する一連のレジストリ関数が定義されています。 これらの関数は構成データを適切なレジストリに直接設定するため、サーバーがクラスター化されているかどうかを印刷モニターで判断する必要はありません。 印刷モニターは、Win32 registry API またはクラスターレジストリ API を直接使用することはできません。すべての構成データは、スプーラのレジストリ機能を使用して保存およびアクセスする必要があります。 スプーラーがモニターの[**InitializePrintMonitor2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitor2)関数を呼び出すと、これらの関数のアドレスが[**monitorreg**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/ns-winsplp-_monitorreg)構造体内の印刷モニターに提供されます。

サーバークラスターでは、スプーラの複数のインスタンスを共存させることができます。 具体的には、各クラスターノードが独自のインスタンスを所有し、クラスター自体に追加のインスタンスが存在します。 スプーラレジストリ関数の入力パラメーターの1つはスプーラハンドルです。 このハンドルは、モニターの**InitializePrintMonitor2**関数によって受信され、モニターを開いたスプーラインスタンス (ノードまたはクラスター) を識別します。 スプーラハンドルを使用すると、スプーラレジストリ関数は各スプーラインスタンスのサブキーを維持します。

 

 




