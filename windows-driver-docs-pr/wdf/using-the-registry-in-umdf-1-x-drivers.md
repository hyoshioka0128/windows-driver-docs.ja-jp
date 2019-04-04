---
title: UMDF 1.x のドライバーのレジストリを使用してください。
description: UMDF 1.x のドライバーのレジストリを使用してください。
ms.assetid: 653f996a-9fc8-461f-b284-a5d6795259d6
keywords:
- レジストリ WDK UMDF
- プロパティ ストア オブジェクト WDK UMDF
- UMDF ドライバー WDK UMDF、レジストリ
- ユーザー モード ドライバー WDK UMDF、レジストリ
- UMDF WDK、レジストリ
- ユーザー モード ドライバー フレームワーク WDK、レジストリ
- WDK UMDF キー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1692fe57bbe69e84c36f58c573537d1da93eb55a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529451"
---
# <a name="using-the-registry-in-umdf-1x-drivers"></a>UMDF 1.x のドライバーのレジストリを使用してください。


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

UMDF ベースのドライバーでは、読み取るでき、プロパティ ストア オブジェクトのインターフェイスを使用して、レジストリの値を記述することができます。

UMDF ベースのドライバーは、4 種類のレジストリ キーにアクセスできます。 ドライバーは、作成、読み取り、およびサブキーとこれらのキーの下の値を書き込むことができます。 次の種類のレジストリ キーは UMDF ベースのドライバーを使用できます。

- ハードウェア キー

  PnP マネージャーがハードウェア キーを作成または*デバイス キー*、デバイスごとに、デバイスの一意な識別情報を格納します。

  ドライバーでは、取得でき、一部のハードウェア キーのプロパティ値を変更することができます。 格納された値の場所は、それらへのアクセスに使用する方法によって異なります。

  プロパティ ストア メソッドを使用して作成されたプロパティの値に格納されます、 **\\デバイス パラメーター**ハードウェア キーの下のサブキー。 これらのプロパティにアクセスするには、ドライバーは、プロパティ ストアのインターフェイスを取得する次のメソッドのいずれかを呼び出します。

  <a href="" id="iwdfdevice--retrievedevicepropertystore"></a>[**IWDFDevice::RetrieveDevicePropertyStore**](https://msdn.microsoft.com/library/windows/hardware/ff558842)  
  ポインターを取得、 [ **IWDFNamedPropertyStore** ](https://msdn.microsoft.com/library/windows/hardware/ff560164)インターフェイス。

  <a href="" id="iwdfdeviceinitialize--retrievedevicepropertystore"></a>[**IWDFDeviceInitialize::RetrieveDevicePropertyStore**](https://msdn.microsoft.com/library/windows/hardware/ff556982)  
  ポインターを取得、 [ **IWDFNamedPropertyStore** ](https://msdn.microsoft.com/library/windows/hardware/ff560164)インターフェイス。

  <a href="" id="iwdfpropertystorefactory--retrievedevicepropertystore"></a>[**IWDFPropertyStoreFactory::RetrieveDevicePropertyStore**](https://msdn.microsoft.com/library/windows/hardware/ff560228)  
  ポインターを取得、 [ **IWDFNamedPropertyStore2** ](https://msdn.microsoft.com/library/windows/hardware/ff560168)インターフェイス。 使用することができます、 *SubkeyPath*など、ドライバーが作成したサブキーの下の値を指定するパラメーター **\\デバイス パラメーター\\**<em>DriverServiceName\\サブキー</em>します。

  ドライバーは、内の値を読み取り専用のアクセス権を持つ、 **\\デバイス パラメーター**サブキーとにアクセスできない**\\デバイス パラメーター\\WDF**または**\\デバイス パラメーター\\WUDF**します。

  デバイス プロパティの統一モデルを使用して作成されたプロパティ値が格納されている、 **\\プロパティ**ハードウェア キーの下のサブキー。

  ドライバーの呼び出し、これらのプロパティにアクセスする[ **IWDFUnifiedPropertyStoreFactory::RetrieveUnifiedDevicePropertyStore** ](https://msdn.microsoft.com/library/windows/hardware/hh451406)プロパティ ストアのインターフェイスを取得します。 ドライバーが使用することができます、 [ **IWDFUnifiedPropertyStore** ](https://msdn.microsoft.com/library/windows/hardware/hh451399)インターフェイスを変更し、デバイスのプロパティの現在の設定を取得します。

- ソフトウェア キー

  ドライバーのソフトウェア キーとも呼ばれますが、*ドライバー キー*レジストリには、各ドライバー ソフトウェア キーが含まれています。 レジストリにデバイスのクラスのすべての一覧が含まれていますされ、そのデバイス クラスのエントリの下に各ドライバーのソフトウェアのキーが存在します。 システムでは、そのソフトウェア キーの下には、各ドライバーに関する情報を格納します。

  ドライバーを呼び出すことができます[ **IWDFPropertyStoreFactory::RetrieveDevicePropertyStore** ](https://msdn.microsoft.com/library/windows/hardware/ff560228)読み取りまたは書き込みアクセスをそのソフトウェア キーの値を取得します。 ドライバーは、特定のデバイスに関連付けられていないドライバー固有の情報を読み書きすることができます。

- デバイス インターフェイス キー

  レジストリにはすべてのキーが含まれています、[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)ドライバーが作成されていること。 これらの各キーの下で、ドライバーが登録されているデバイスのインターフェイス クラスの各インスタンスのエントリです。

  読み取り/呼び出すことによって、そのインスタンスのレジストリのエントリの値を書き込むことができる場合、ドライバーには、デバイスのインターフェイス クラスのインスタンスが登録されているが、 [ **IWDFPropertyStoreFactory::RetrieveDevicePropertyStore**](https://msdn.microsoft.com/library/windows/hardware/ff560228). ドライバーは、デバイス インターフェイスのインスタンスに固有の情報を読み書きすることができます。

- **DEVICEMAP**キー

  レジストリが含まれています、 **HKEY\_ローカル\_マシン\\ハードウェア\\DEVICEMAP**シリアルおよびパラレル ポートなどの以前のテクノロジの一部のドライバーを使用するキー。 ドライバーを使用するテクノロジをサポートしている場合、 **DEVICEMAP**キー、ドライバー アクセスできるサブキーと、キーの値を呼び出して[ **IWDFPropertyStoreFactory::RetrieveDevicePropertyStore**](https://msdn.microsoft.com/library/windows/hardware/ff560228).

いずれかのドライバーが呼び出された後、 **RetrieveDevicePropertyStore**ドライバーのレジストリ サブキーを開くメソッドによって公開されるメソッドを使用できます[ **IWDFNamedPropertyStore** ](https://msdn.microsoft.com/library/windows/hardware/ff560164)、 [ **IWDFNamedPropertyStore2**](https://msdn.microsoft.com/library/windows/hardware/ff560168)、または[ **IWDFUnifiedPropertyStore** ](https://msdn.microsoft.com/library/windows/hardware/hh451399)作成、読み取り、および下の値を書き込むにはサブキー。 **IWDFNamedPropertyStore2**インターフェイスは、値を削除するドライバーもできます。

ドライバーのレジストリ キーの詳細については、[レジストリ ツリーの概要とキー](https://msdn.microsoft.com/library/windows/hardware/ff549538)を参照してください。

 

 





