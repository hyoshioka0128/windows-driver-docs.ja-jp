---
title: インストールされているデバイスインターフェイスの列挙
description: インストールされているデバイスインターフェイスの列挙
ms.assetid: 14A9E6DD-58A9-4af0-B469-7CCF4596BE27
keywords:
- インストールされているデバイスインターフェイスの列挙 WDK
- インストールされているデバイスインターフェイス WDK
- インストールされているデバイスインターフェイス WDK、列挙
- デバイスインターフェイス WDK デバイスのインストール、列挙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9d30aa6ebe1e1aaa588b89278e98107e8ba4c22
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840636"
---
# <a name="enumerating-installed-device-interfaces"></a>インストールされているデバイスインターフェイスの列挙


レジストリキーに直接アクセスすることによって、システム内のデバイスインターフェイスクラスを列挙することはできません。 レジストリキーと同様に、キーの場所、名前、または形式は、Windows の異なるバージョン間で変更される可能性があります。

デバイスインターフェイスの属性を安全に検出するには、次のガイドラインに従います。

-   ユーザーモードアプリケーションは、次の手順に従う必要があります。

    1.  指定されたデバイスインターフェイスクラスのインターフェイスをサポートするデバイスを取得するには、 [**SetupDiGetClassDevs**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)または[**Setupdigetclassdevsex**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa)を使用します。 *Flags*パラメーターに DIGCF_DEVICEINTERFACE フラグを設定し、*列挙子*パラメーターを特定のデバイスインスタンス識別子に設定する必要があります。

        システム内に存在するデバイスインターフェイスだけを含めるには、 *Flags*パラメーターに DIGCF_PRESENT フラグを設定します。

    2.  [**Setupdienumdeviceinterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)を使用して、デバイスインターフェイスクラスに登録されているインターフェイスを列挙します。 このインターフェイスクラスは、 *InterfaceClassGuid*パラメーターを使用して指定します。

-   カーネルモードドライバーでは、 [**Iogetdeviceinterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfaces)を使用して、システムにインストールされているデバイスインターフェイスクラスを列挙する必要があります。

 

 





