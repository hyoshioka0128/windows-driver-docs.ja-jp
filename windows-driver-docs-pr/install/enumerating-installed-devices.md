---
title: インストールされているデバイスを列挙します。
description: インストールされているデバイスを列挙します。
ms.assetid: 98EF9A16-6415-4778-BB5D-C0B7160C1509
keywords:
- インストールされているデバイス WDK の列挙
- インストールされているデバイス、WDK を列挙します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2fdbc37e48a6b6428ac08e017e1e68c6f7c78e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528482"
---
# <a name="enumerating-installed-devices"></a>インストールされているデバイスを列挙します。


レジストリ キーを直接使用してデバイスを列挙する必要がありますできません。 レジストリ キーでは、システムにインストールされているデバイスを列挙するために必要な情報は含まれません。 など、デバイスが実際に存在するかはファントムのデバイス (1 つに接続されていない)、この情報が保持している、[プラグ アンド プレイ (PnP) manager](pnp-manager.md)します。 PnP マネージャーでは、レジストリ情報の追加のフィルター処理も実行します。

インストールされているデバイスを安全に列挙するには、次の手順に従います。

1.  使用[ **SetupDiGetClassDevs** ](https://msdn.microsoft.com/library/windows/hardware/ff551069)または[ **SetupDiGetClassDevsEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551072)一連の指定したに属しているデバイスの情報を取得するにはデバイス セットアップ クラス。 システムに存在するデバイスに対してのみ情報を取得するで DIGCF_PRESENT を設定、*フラグ*パラメーター。

2.  使用[ **SetupDiEnumDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff551010)セット内のデバイスを列挙します。

3.  使用[ **SetupDiGetDeviceInstanceId** ](https://msdn.microsoft.com/library/windows/hardware/ff551106)一意を取得する[デバイス インスタンス識別子 (Id)](device-instance-ids.md)します。

 

 





