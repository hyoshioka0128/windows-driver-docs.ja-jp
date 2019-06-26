---
title: インストール済みのデバイス インターフェイスの列挙
description: インストール済みのデバイス インターフェイスの列挙
ms.assetid: 14A9E6DD-58A9-4af0-B469-7CCF4596BE27
keywords:
- デバイス インターフェイス WDK をインストールを列挙します。
- デバイス インターフェイス WDK をインストールします。
- デバイスのインターフェイス、WDK をインストールを列挙します。
- デバイス インターフェイスの列挙、WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0fcdfcd59a549049e2a465f057f56cb1f4b574d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379477"
---
# <a name="enumerating-installed-device-interfaces"></a>インストール済みのデバイス インターフェイスの列挙


レジストリ キーに直接アクセスするシステムでデバイスのインターフェイス クラスを列挙する必要がありますできません。 任意のレジストリ キーと同様、場所、名、またはキーの形式が Windows の異なるバージョン間変更可能性があります。

安全にデバイスのインターフェイスの属性を検出するのにには、次のガイドラインを使用します。

-   ユーザー モード アプリケーションは、次の手順に従う必要があります。

    1.  使用[ **SetupDiGetClassDevs** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)または[ **SetupDiGetClassDevsEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa)指定されたインターフェイスをサポートするデバイスを取得するにはデバイス インターフェイスのクラスです。 DIGCF_DEVICEINTERFACE フラグを設定する必要があります、*フラグ*して、パラメーターを設定する必要があります、*列挙子*パラメーターを特定のデバイスのインスタンス識別子。

        システムに存在するデバイスのインターフェイスのみを含める DIGCF_PRESENT フラグを設定します。、*フラグ*パラメーター。

    2.  使用[ **SetupDiEnumDeviceInterfaces** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)デバイス インターフェイスのクラスに登録されているインターフェイスを列挙します。 このインターフェイスのクラスがで指定された、 *InterfaceClassGuid*パラメーター。

-   カーネル モード ドライバーを使用する必要があります[ **IoGetDeviceInterfaces** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceinterfaces)システムにインストールされているデバイスのインターフェイス クラスを列挙します。

 

 





