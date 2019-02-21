---
title: レジストリにデバイス オブジェクトのプロパティを設定します。
description: レジストリにデバイス オブジェクトのプロパティを設定します。
ms.assetid: a2cfe098-0d5d-42fb-bbdc-25376ce50a9b
keywords:
- デバイス オブジェクトの WDK カーネル、レジストリ
- レジストリの WDK デバイス オブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: de830ef6bae0a979b7447ccbc0e1710bdb7c3592
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529298"
---
# <a name="setting-device-object-properties-in-the-registry"></a>レジストリにデバイス オブジェクトのプロパティを設定します。





デバイス オブジェクトのプロパティは、次のように、レジストリで設定できます。

-   WDM ドライバー、または全体のデバイス セットアップ クラスに対するデバイスのモデルごとにプロパティを設定することができます。 (デバイス セットアップ クラスの詳細については、次を参照してください[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)。)。

-   非 WDM ドライバーでは、名前付きのデバイス オブジェクトのデバイス セットアップ クラスのプロパティを設定できます。 デバイス オブジェクトを作成するときに、ドライバーはデバイス セットアップ クラスを指定します**IoCreateDeviceSecure**します。 デバイス セットアップ クラスを指定する方法の詳細については、次を参照してください。 [ **IoCreateDeviceSecure**](https://msdn.microsoft.com/library/windows/hardware/ff548407)します。

レジストリ内のすべての設定は、ドライバーのデバイス オブジェクトを作成するときに指定するプロパティをオーバーライドします。

レジストリ設定は、デバイスのインストール中に使用される INF ファイルで指定されたかを呼び出すアプリケーションをインストール後に指定することができます、[デバイスのインストール機能](https://msdn.microsoft.com/library/windows/hardware/ff541299)します。

このセクションには、次のサブセクションが含まれています。

[インストール中にデバイス オブジェクトのレジストリのプロパティを設定します。](setting-device-object-registry-properties-during-installation.md)

[インストール後にデバイス オブジェクトのレジストリのプロパティを設定します。](setting-device-object-registry-properties-after-installation.md)

 

 




