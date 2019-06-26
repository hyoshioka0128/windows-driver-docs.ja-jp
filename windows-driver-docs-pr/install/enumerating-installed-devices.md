---
title: インストール済みのデバイスの列挙
description: インストール済みのデバイスの列挙
ms.assetid: 98EF9A16-6415-4778-BB5D-C0B7160C1509
keywords:
- インストールされているデバイス WDK の列挙
- インストールされているデバイス、WDK を列挙します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 817033cd9b6f49b01e36cb408f6c527dd0d969ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379472"
---
# <a name="enumerating-installed-devices"></a>インストール済みのデバイスの列挙


レジストリ キーを直接使用してデバイスを列挙する必要がありますできません。 レジストリ キーでは、システムにインストールされているデバイスを列挙するために必要な情報は含まれません。 など、デバイスが実際に存在するかはファントムのデバイス (1 つに接続されていない)、この情報が保持している、[プラグ アンド プレイ (PnP) manager](pnp-manager.md)します。 PnP マネージャーでは、レジストリ情報の追加のフィルター処理も実行します。

インストールされているデバイスを安全に列挙するには、次の手順に従います。

1.  使用[ **SetupDiGetClassDevs** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)または[ **SetupDiGetClassDevsEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa)一連の指定したに属しているデバイスの情報を取得するにはデバイス セットアップ クラス。 システムに存在するデバイスに対してのみ情報を取得するで DIGCF_PRESENT を設定、*フラグ*パラメーター。

2.  使用[ **SetupDiEnumDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinfo)セット内のデバイスを列挙します。

3.  使用[ **SetupDiGetDeviceInstanceId** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinstanceida)一意を取得する[デバイス インスタンス識別子 (Id)](device-instance-ids.md)します。

 

 





