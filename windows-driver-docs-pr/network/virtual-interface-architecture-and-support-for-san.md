---
title: 仮想インターフェイス アーキテクチャと SAN のサポート
description: 仮想インターフェイス アーキテクチャと SAN のサポート
ms.assetid: 83d28f33-7354-4f59-8b01-4842286f12fb
keywords:
- システム エリア ネットワーク WDK、VI アーキテクチャ
- SAN の WDK、VI アーキテクチャ
- VI アーキテクチャ WDK San
- 仮想インターフェイス アーキテクチャ WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6448456a819ba9501651ad91bdcde40e85d7e01
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582121"
---
# <a name="virtual-interface-architecture-and-support-for-san"></a>仮想インターフェイス アーキテクチャと SAN のサポート





Compaq、Intel、および、Microsoft によって提案された、仮想インターフェイス (VI) アーキテクチャは、SAN NIC とホスト コンピューターのシステム間のインターフェイスの設計です。 このアーキテクチャでは、デザインに関してシステム エリア ネットワーク (SAN) の 1 つの側面を表します。 同じ基本的な特性を共有する別の設計があります。

VI アーキテクチャは、SAN の相互接続用に一連の機能と特性を定義します。 たとえば、VI アーキテクチャには、リモート ダイレクト メモリ アクセス (RDMA) の操作のサポートが含まれています。 VI アーキテクチャでは、エンドポイントとの接続を管理して、データ転送の要求を処理、SAN NIC と対話するための特定のメカニズムについても説明します。

VI アーキテクチャを使用するもの以外に SAN の広範なクラスでの Windows Sockets スイッチの動作が相互接続します。 Windows ソケットに SAN の拡張機能は、特定の SAN NIC のプロバイダー インターフェイス (SPI) シールド ハードウェア インターフェイスからスイッチをサービスします。 そのハードウェア インターフェイスが SAN サービス プロバイダーの DLL とそのカーネル モードのプロキシ ドライバー内でカプセル化されます。 これらのコンポーネントは、SAN ベンダーによって提供されます。 SAN の拡張機能の詳細については、[Windows Sockets SPI Extensions for San](windows-sockets-spi-extensions-for-sans.md)を参照してください。

 

 





