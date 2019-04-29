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
ms.openlocfilehash: 4ea0698accf70230a3a9fc08cb7a202376ba17ba
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386990"
---
# <a name="enumerating-installed-device-interfaces"></a>インストール済みのデバイス インターフェイスの列挙


レジストリ キーに直接アクセスするシステムでデバイスのインターフェイス クラスを列挙する必要がありますできません。 任意のレジストリ キーと同様、場所、名、またはキーの形式が Windows の異なるバージョン間変更可能性があります。

安全にデバイスのインターフェイスの属性を検出するのにには、次のガイドラインを使用します。

-   ユーザー モード アプリケーションは、次の手順に従う必要があります。

    1.  使用[ **SetupDiGetClassDevs** ](https://msdn.microsoft.com/library/windows/hardware/ff551069)または[ **SetupDiGetClassDevsEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551072)指定されたインターフェイスをサポートするデバイスを取得するにはデバイス インターフェイスのクラスです。 DIGCF_DEVICEINTERFACE フラグを設定する必要があります、*フラグ*して、パラメーターを設定する必要があります、*列挙子*パラメーターを特定のデバイスのインスタンス識別子。

        システムに存在するデバイスのインターフェイスのみを含める DIGCF_PRESENT フラグを設定します。、*フラグ*パラメーター。

    2.  使用[ **SetupDiEnumDeviceInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff551015)デバイス インターフェイスのクラスに登録されているインターフェイスを列挙します。 このインターフェイスのクラスがで指定された、 *InterfaceClassGuid*パラメーター。

-   カーネル モード ドライバーを使用する必要があります[ **IoGetDeviceInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff549186)システムにインストールされているデバイスのインターフェイス クラスを列挙します。

 

 





