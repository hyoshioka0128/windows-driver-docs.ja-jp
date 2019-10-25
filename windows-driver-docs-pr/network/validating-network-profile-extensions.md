---
title: ネットワーク プロファイル拡張機能の検証
description: ネットワーク プロファイル拡張機能の検証
ms.assetid: d29805a3-7ecb-4587-99c5-b1f8ad9f1503
keywords:
- ネットワークプロファイル WDK ネイティブ 802.11 IHV 拡張 DLL、拡張機能の検証
- ネットワークプロファイル拡張機能の検証 WDK ネイティブ 802.11 IHV 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa128eb19305deaf2c31035269a4a992bcd8e709
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842964"
---
# <a name="validating-network-profile-extensions"></a>ネットワーク プロファイル拡張機能の検証




 

オペレーティングシステムは、次の条件下で ihv が定義した接続とセキュリティ設定を検証するために、IHV ハンドラ関数を呼び出します。

-   ユーザーは、IHV が定義した接続またはセキュリティプロファイルの拡張機能の設定を含む新しいネットワークプロファイルを作成します。 このような状況では、オペレーティングシステムは[*Dot11ExtIhvValidateProfile*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_validate_profile) IHV ハンドラー関数を呼び出してユーザー設定を検証します。

-   WLAN アダプタはスキャン操作を完了し、結果をオペレーティングシステムに返します。 オペレーティングシステムは、 [*Dot11ExtIhvPerformCapabilityMatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_capability_match) ihv ハンドラー関数を呼び出して、検出された基本サービスセット (BSS) ネットワークがネットワークプロファイルからの IHV 定義の接続とセキュリティ設定と一致するかどうかを判断します。

    オペレーティングシステムは、BSS ネットワークから**Dot1ExtIhvPerformCapabilityMatch**関数の*p tablebssid*パラメーターに802.11 ビーコンおよびプローブ応答フレームの一覧を渡します。 また、オペレーティングシステムは、接続とセキュリティプロファイルの拡張機能を、それぞれ*Pihvconnprofile*と*Pihvconnprofile*パラメーターに渡します。

    802.11 ビーコンおよびプローブ応答フレームのリストに含まれるすべてのエントリが、プロファイルフラグメントに定義されている接続とセキュリティ属性をアドバタイズする場合、 [*Dot11ExtIhvPerformCapabilityMatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_capability_match)関数はエラー\_成功を返します。

-   オペレーティングシステムは、 [*Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)関数を呼び出して、関連付け前の操作を開始します。 この場合、IHV 拡張 DLL は、接続とセキュリティの設定が有効であることを確認する必要があります。 設定が有効な場合、関数は成功\_エラーを返し、DLL は関連付け前の操作を続行します。 それ以外の場合、関数は Winerror.h で定義されている適切なエラーコードを返します。

    事前関連付け操作の詳細については、「[事前関連付け操作](pre-association-operations.md)」を参照してください。

IHV ハンドラー関数の詳細については、「[ネイティブ 802.11 Ihv ハンドラー関数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-handler-functions)」を参照してください。

 

 





