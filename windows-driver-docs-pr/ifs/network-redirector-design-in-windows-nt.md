---
title: Windows NT におけるネットワーク リダイレクターの設計
description: Windows NT におけるネットワーク リダイレクターの設計
ms.assetid: 1feb43a3-ee65-4446-b38b-8b3f9188f43d
keywords:
- ネットワーク リダイレクター WDK、Windows NT
- リダイレクター ドライバー WDK、Windows NT
- カーネル ネットワーク リダイレクター WDK、Windows NT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec0c50183bb7820bab4d93114102aa6d203f9606
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573405"
---
# <a name="network-redirector-design-in-windows-nt"></a>Windows NT におけるネットワーク リダイレクターの設計


## <span id="ddk_network_redirector_design_in_windows_nt_if"></span><span id="DDK_NETWORK_REDIRECTOR_DESIGN_IN_WINDOWS_NT_IF"></span>


ネットワーク リダイレクターのカーネル モード ドライバーを実装するアーキテクチャは、時間の経過と共に変更されました。 ネットワーク リダイレクターの一般的なモデルは通常 Microsoft ネットワーク (LAN Manager のクライアント) クライアントのカーネル ドライバーを実装するアーキテクチャに基づいています。 Windows NT 3.0 で導入された元のスキームを使用して、共有コンポーネントは使用されずが限られていました。 このモデルは、元の rdr ドライバー モデルと呼ばれる多くの場合、(rdr がリダイレクターの省略形)。 ネットワーク リダイレクターを作成するプロセスを簡略化する、オペレーティング システムからの特別なサポートが提供されません。 各カーネル モード ドライバーには、すべてのネットワーク リダイレクターに必要な関数が実装されています。 その結果、各カーネル ドライバーには、大量 I/O マネージャー、キャッシュ マネージャー、およびメモリ マネージャーとのやり取りのコードにはが含まれます。 Windows にインストールする各ネットワーク リダイレクター (LAN Manager、NetWare、および例については、NFS) は、これらの関数自体のすべてを実装する必要があります。 この設計モデルは、Windows NT 4.0 でのネットワーク リダイレクター ドライバーに使用されました。 このアーキテクチャで、複数のリダイレクターのダイアグラムを次に示します。

![windows nt でネットワーク リダイレクター デザインを示す図](images/redir-01.png)

 

 




