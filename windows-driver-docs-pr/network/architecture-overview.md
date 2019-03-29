---
title: ネットワーク モジュールのレジストラーのアーキテクチャの概要
description: ネットワーク モジュールのレジストラーの基本的なアーキテクチャの概要を説明します。
ms.assetid: 7e2c51ed-ecec-4b17-8a6f-42a51acedc95
keywords:
- ネットワーク モジュールのレジストラー WDK、アーキテクチャ
- NMR WDK、アーキテクチャ
- WDK ネットワーク モジュールのレジストラーのアーキテクチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c51a73444c120d20889f728877da5bdbd6467b1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574433"
---
# <a name="architecture-overview-for-the-network-module-registrar"></a>ネットワーク モジュールのレジストラーのアーキテクチャの概要

ネットワーク モジュール レジストラー (NMR) の基本的なアーキテクチャの概要については、次の図に示されます。

![ネットワーク モジュール レジストラー (nmr) の基本的なアーキテクチャを示す図](images/nmrarch.png)

このような状況では、2 つ[モジュールをネットワーク](network-module.md)、[クライアント モジュール](client-module.md)と[プロバイダー モジュール](provider-module.md)します。 クライアントのモジュールとプロバイダー、モジュールはそれぞれ、クライアントと同じプロバイダー[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md)します。 各ネットワーク モジュールは登録 NMR と直接対話し、だけでなくへのアタッチ、およびその他のネットワーク モジュールからのデタッチ、登録解除します。 同じ NPI がサポートする場合にのみ、クライアント モジュールをプロバイダー モジュールにアタッチ、NMR が開始されます。 クライアント モジュールとプロバイダー、モジュールが相互に接続されると、NMR の独立した、NPI 関数を使用して相互作用することができます。

次のセクションでは、によってクライアント モジュールと、一般的な NPI は両方ともサポートするプロバイダー モジュールがアタッチされてとデタッチされたプロセスの概要を示します。

[ネットワーク モジュールの添付ファイル](network-module-attachment.md)

[ネットワーク モジュールのデタッチ](network-module-detachment.md)

 

 





