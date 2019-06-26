---
title: ネットワーク プロファイル拡張機能の検証
description: ネットワーク プロファイル拡張機能の検証
ms.assetid: d29805a3-7ecb-4587-99c5-b1f8ad9f1503
keywords:
- ネットワーク プロファイルの WDK ネイティブ 802.11 IHV 拡張機能の DLL、拡張機能を検証しています
- ネットワーク プロファイルの拡張機能 WDK の 802.11 IHV ・拡張機能のネイティブ DLL を検証しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e46953bcff1b4032b0d0f3891a3567aad2bd2a6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384361"
---
# <a name="validating-network-profile-extensions"></a>ネットワーク プロファイル拡張機能の検証




 

オペレーティング システムでは、次の条件下で、IHV 定義の接続とセキュリティ設定を検証する IHV ハンドラー関数を呼び出します。

-   ユーザーは、IHV 定義の接続やセキュリティ プロファイルの拡張機能の設定を含む新しいネットワーク プロファイルを作成します。 このような状況でオペレーティング システムの呼び出し、 [ *Dot11ExtIhvValidateProfile* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_validate_profile)ユーザー設定を検証する IHV ハンドラー関数。

-   WLAN アダプターでは、スキャン操作を完了し、オペレーティング システムにその結果を返します。 オペレーティング システムの呼び出し、 [ *Dot11ExtIhvPerformCapabilityMatch* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_capability_match) IHV ハンドラー関数を IHV で定義された接続の一致するネットワークが検出された基本的なサービス (BSS) を設定するかどうかを判断し、ネットワーク プロファイルのセキュリティ設定。

    オペレーティング システムでは、ビーコンおよびプローブ応答の 802.11 フレームの一覧を渡します BSS ネットワークから、 *pConnectableBssid*のパラメーター、 **Dot1ExtIhvPerformCapabilityMatch**関数。 オペレーティング システムにも渡す接続とセキュリティ プロファイルの拡張機能、 *pIhvConnProfile*と*pIhvSecProfile*パラメーター、それぞれします。

    プロファイルのフラグメントで定義されている接続とセキュリティの属性をアドバタイズすべてビーコンおよびプローブ応答の 802.11 フレームのリストのエントリの場合、 [ *Dot11ExtIhvPerformCapabilityMatch* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_capability_match)関数には、エラーが返されます。\_成功します。

-   オペレーティング システムを呼び出して関連付け前の操作を開始する、 [ *Dot11ExtIhvPerformPreAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)関数。 このような状況で IHV 拡張機能の DLL をする必要があります、接続およびセキュリティ設定が有効である確認します。 関数にエラーが返されます、設定が有効な場合は、\_成功と DLL は、関連付け前の操作を続行します。 それ以外の場合、関数は、Winerror.h で定義されている、該当するエラー コードを返します。

    前の関連付け操作の詳細については、次を参照してください。[関連付け前操作](pre-association-operations.md)します。

IHV ハンドラー関数の詳細については、次を参照してください。 [802.11 IHV ハンドラー関数をネイティブ](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-handler-functions)します。

 

 





