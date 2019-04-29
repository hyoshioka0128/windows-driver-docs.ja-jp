---
title: レジストリでのデバイス オブジェクトのプロパティの設定
description: レジストリでのデバイス オブジェクトのプロパティの設定
ms.assetid: a2cfe098-0d5d-42fb-bbdc-25376ce50a9b
keywords:
- デバイス オブジェクトの WDK カーネル、レジストリ
- レジストリの WDK デバイス オブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: de830ef6bae0a979b7447ccbc0e1710bdb7c3592
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385533"
---
# <a name="setting-device-object-properties-in-the-registry"></a>レジストリでのデバイス オブジェクトのプロパティの設定





デバイス オブジェクトのプロパティは、次のように、レジストリで設定できます。

-   WDM ドライバー、または全体のデバイス セットアップ クラスに対するデバイスのモデルごとにプロパティを設定することができます。 (デバイス セットアップ クラスの詳細については、次を参照してください[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)。)。

-   非 WDM ドライバーでは、名前付きのデバイス オブジェクトのデバイス セットアップ クラスのプロパティを設定できます。 デバイス オブジェクトを作成するときに、ドライバーはデバイス セットアップ クラスを指定します**IoCreateDeviceSecure**します。 デバイス セットアップ クラスを指定する方法の詳細については、次を参照してください。 [ **IoCreateDeviceSecure**](https://msdn.microsoft.com/library/windows/hardware/ff548407)します。

レジストリ内のすべての設定は、ドライバーのデバイス オブジェクトを作成するときに指定するプロパティをオーバーライドします。

レジストリ設定は、デバイスのインストール中に使用される INF ファイルで指定されたかを呼び出すアプリケーションをインストール後に指定することができます、[デバイスのインストール機能](https://msdn.microsoft.com/library/windows/hardware/ff541299)します。

このセクションには、次のサブセクションが含まれています。

[インストール中にデバイス オブジェクトのレジストリのプロパティを設定します。](setting-device-object-registry-properties-during-installation.md)

[インストール後にデバイス オブジェクトのレジストリのプロパティを設定します。](setting-device-object-registry-properties-after-installation.md)

 

 




