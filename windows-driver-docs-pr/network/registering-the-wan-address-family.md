---
title: WAN のアドレス ファミリを登録します。
description: WAN のアドレス ファミリを登録します。
ms.assetid: 31443e99-24d8-4276-8345-004b0eeb05d7
keywords:
- いる CoNDIS WAN ドライバー WDK ネットワーク、TAPI アドレス ファミリ
- NdisCmRegisterAddressFamilyEx
- TAPI WDK のネットワーク
- WAN のアドレス ファミリを登録します。
- WAN のアドレス ファミリの WDK ネットワーク
- アドレス ファミリの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4cfa400020fcd2640786a3af4930420e9d78938
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552367"
---
# <a name="registering-the-wan-address-family"></a>WAN のアドレス ファミリを登録します。





このトピックでは、いる CoNDIS WAN ミニポート コール マネージャー (MCM) または別個の呼び出しマネージャーから TAPI アドレス ファミリを登録する方法について説明します。

コール マネージャーの呼び出しのいずれかの種類、 [ **NdisCmRegisterAddressFamilyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff561685)関数のコール マネージャーのエントリ ポイントと、アドレス ファミリの種類 CO を登録する\_アドレス\_ファミリ\_TAPI\_プロキシ。 これによりは、ドライバーは、TAPI サービスを提供することを示します。 いる CoNDIS ドライバーでは、アドレス ファミリの登録に関する詳細については、次を参照してください。[を登録すると、アドレス ファミリを開く](registering-and-opening-an-address-family.md)します。

NDIS は、新しく登録されたアドレス ファミリの NDPROXY を通知します。 NDPROXY は、コール マネージャーが提供する TAPI サービスを使用できることを決定します。 NDPROXY は、ドライバーに関連付けられ、NDIS NDPROXY の接続指向のエントリ ポイントに登録する TAPI プロキシ アドレス ファミリが表示されます。 これらのエントリ ポイントは、ドライバーとの通信に使用されます。

NDPROXY は、ミニポート ドライバーの TAPI 機能を列挙し、後で NDIS 構造にカプセル化される TAPI 要求を送信できます。 TAPI サポートいる CoNDIS 拡張機能の使用に関する詳細については、次を参照してください。[いる CoNDIS WAN 操作をサポート電話サービス](condis-wan-operations-that-support-telephonic-services.md)します。

 

 





