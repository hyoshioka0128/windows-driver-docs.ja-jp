---
title: ネットワーク プロファイル拡張機能の検証
description: ネットワーク プロファイル拡張機能の検証
ms.assetid: d29805a3-7ecb-4587-99c5-b1f8ad9f1503
keywords:
- ネットワーク プロファイルの WDK ネイティブ 802.11 IHV 拡張機能の DLL、拡張機能を検証しています
- ネットワーク プロファイルの拡張機能 WDK の 802.11 IHV ・拡張機能のネイティブ DLL を検証しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52e01b65932935224b6e9f823d3d33fa973758b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573875"
---
# <a name="validating-network-profile-extensions"></a>ネットワーク プロファイル拡張機能の検証




 

オペレーティング システムでは、次の条件下で、IHV 定義の接続とセキュリティ設定を検証する IHV ハンドラー関数を呼び出します。

-   ユーザーは、IHV 定義の接続やセキュリティ プロファイルの拡張機能の設定を含む新しいネットワーク プロファイルを作成します。 このような状況でオペレーティング システムの呼び出し、 [ *Dot11ExtIhvValidateProfile* ](https://msdn.microsoft.com/library/windows/hardware/ff547523)ユーザー設定を検証する IHV ハンドラー関数。

-   WLAN アダプターでは、スキャン操作を完了し、オペレーティング システムにその結果を返します。 オペレーティング システムの呼び出し、 [ *Dot11ExtIhvPerformCapabilityMatch* ](https://msdn.microsoft.com/library/windows/hardware/ff547488) IHV ハンドラー関数を IHV で定義された接続の一致するネットワークが検出された基本的なサービス (BSS) を設定するかどうかを判断し、ネットワーク プロファイルのセキュリティ設定。

    オペレーティング システムでは、ビーコンおよびプローブ応答の 802.11 フレームの一覧を渡します BSS ネットワークから、 *pConnectableBssid*のパラメーター、 **Dot1ExtIhvPerformCapabilityMatch**関数。 オペレーティング システムにも渡す接続とセキュリティ プロファイルの拡張機能、 *pIhvConnProfile*と*pIhvSecProfile*パラメーター、それぞれします。

    プロファイルのフラグメントで定義されている接続とセキュリティの属性をアドバタイズすべてビーコンおよびプローブ応答の 802.11 フレームのリストのエントリの場合、 [ *Dot11ExtIhvPerformCapabilityMatch* ](https://msdn.microsoft.com/library/windows/hardware/ff547488)関数には、エラーが返されます。\_成功します。

-   オペレーティング システムを呼び出して関連付け前の操作を開始する、 [ *Dot11ExtIhvPerformPreAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547499)関数。 このような状況で IHV 拡張機能の DLL をする必要があります、接続およびセキュリティ設定が有効である確認します。 関数にエラーが返されます、設定が有効な場合は、\_成功と DLL は、関連付け前の操作を続行します。 それ以外の場合、関数は、Winerror.h で定義されている、該当するエラー コードを返します。

    前の関連付け操作の詳細については、[関連付け前操作](pre-association-operations.md)を参照してください。

IHV ハンドラー関数の詳細については、[802.11 IHV ハンドラー関数をネイティブ](https://msdn.microsoft.com/library/windows/hardware/ff560627)を参照してください。

 

 





