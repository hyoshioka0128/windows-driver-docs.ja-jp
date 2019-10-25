---
title: レジストリでのデバイス オブジェクトのプロパティの設定
description: レジストリでのデバイス オブジェクトのプロパティの設定
ms.assetid: a2cfe098-0d5d-42fb-bbdc-25376ce50a9b
keywords:
- デバイスオブジェクト WDK カーネル、レジストリ
- レジストリ WDK デバイスオブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02756051369f359ff21a2696000a4457f8cc6d21
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838432"
---
# <a name="setting-device-object-properties-in-the-registry"></a>レジストリでのデバイス オブジェクトのプロパティの設定





デバイスオブジェクトのプロパティは、次のようにレジストリで設定できます。

-   WDM ドライバーの場合、プロパティはデバイスの各モデルに対して、またはデバイスセットアップクラス全体に対して設定できます。 (デバイスセットアップクラスの詳細については、「[デバイスセットアップクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)」を参照してください)。

-   WDM 以外のドライバーの場合は、名前付きデバイスオブジェクトのデバイスセットアップクラスにプロパティを設定できます。 ドライバーでは、 **Iocreateデバイス**を使用してデバイスオブジェクトを作成するときに、デバイスのセットアップクラスを指定します。 デバイスセットアップクラスを指定する方法の詳細については、「 [**Iocreateデバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)」を参照してください。

レジストリ内の設定は、ドライバーがデバイスオブジェクトを作成したときに指定されたプロパティを上書きします。

レジストリ設定は、デバイスのインストール中に使用される INF ファイルによって指定されます。また、[デバイスのインストール機能](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))を呼び出すアプリケーションによってインストール後に指定することもできます。

このセクションには、次のサブセクションが含まれています。

[インストール中にデバイスオブジェクトのレジストリプロパティを設定する](setting-device-object-registry-properties-during-installation.md)

[インストール後にデバイスオブジェクトのレジストリプロパティを設定する](setting-device-object-registry-properties-after-installation.md)

 

 




