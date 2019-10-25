---
title: UMDF 1.x ドライバーでのレジストリの使用
description: UMDF 1.x ドライバーでのレジストリの使用
ms.assetid: 653f996a-9fc8-461f-b284-a5d6795259d6
keywords:
- レジストリ WDK UMDF
- プロパティストアオブジェクト WDK UMDF
- UMDF ドライバー WDK UMDF、registry
- ユーザーモードドライバー WDK UMDF、レジストリ
- UMDF WDK、レジストリ
- ユーザーモードドライバーフレームワーク WDK、レジストリ
- キー WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb7d3efdb734110a86b0c5a3f50d40e09b2b27fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845429"
---
# <a name="using-the-registry-in-umdf-1x-drivers"></a>UMDF 1.x ドライバーでのレジストリの使用


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

UMDF ベースのドライバーは、プロパティストアオブジェクトのインターフェイスを使用して、レジストリ内の値の読み取りと書き込みを行うことができます。

UMDF ベースのドライバーは、4種類のレジストリキーにアクセスできます。 ドライバーは、これらのキーの下にサブキーと値の作成、読み取り、および書き込みを行うことができます。 UMDF ベースのドライバーでは、次の種類のレジストリキーを使用できます。

- ハードウェアキー

  PnP マネージャーは、デバイスごとに、デバイスの一意の識別情報を格納するハードウェアキー (*デバイスキー*) を作成します。

  ドライバーは、ハードウェアキーの下にあるプロパティ値の一部を取得して変更できます。 格納されている値の場所は、それらにアクセスするために使用するメソッドによって異なります。

  PropertyStore メソッドを使用して作成されたプロパティ値は、ハードウェアキーの下の [ **\\デバイスパラメーター** ] サブキーに格納されます。 これらのプロパティにアクセスするために、ドライバーは次のいずれかのメソッドを呼び出して、プロパティストアインターフェイスを取得します。

  <a href="" id="iwdfdevice--retrievedevicepropertystore"></a>[**IWDFDevice:: RetrieveDevicePropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-retrievedevicepropertystore)  
  [**Iwdfnamedpropertystore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfnamedpropertystore)インターフェイスへのポインターを取得します。

  <a href="" id="iwdfdeviceinitialize--retrievedevicepropertystore"></a>[**IWDFDeviceInitialize:: RetrieveDevicePropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-retrievedevicepropertystore)  
  [**Iwdfnamedpropertystore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfnamedpropertystore)インターフェイスへのポインターを取得します。

  <a href="" id="iwdfpropertystorefactory--retrievedevicepropertystore"></a>[**IWDFPropertyStoreFactory::RetrieveDevicePropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfpropertystorefactory-retrievedevicepropertystore)  
  [**IWDFNamedPropertyStore2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfnamedpropertystore2)インターフェイスへのポインターを取得します。 *Subkeypath パス*パラメーターを使用して、ドライバーによって作成されたサブキーの下に値を指定できます。たとえば、 **\\デバイスパラメーター\\** <em>driverservicename\\サブキー</em>です。

  ドライバーは **\\デバイスパラメーター**サブキー内の値への読み取り専用アクセス権を持ち、 **\\デバイスパラメーター\\WDF**または **\\デバイスパラメーター\\wudf**にアクセスすることはできません。

  統合デバイスプロパティモデルを使用して作成されたプロパティ値は、ハードウェアキーの下にある [ **\\Properties** ] サブキーに格納されます。

  これらのプロパティにアクセスするために、ドライバーは[**IWDFUnifiedPropertyStoreFactory:: RetrieveUnifiedDevicePropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfunifiedpropertystorefactory-retrieveunifieddevicepropertystore)を呼び出して、プロパティストアインターフェイスを取得します。 次に、ドライバーは、 [**IWDFUnifiedPropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfunifiedpropertystore)インターフェイスを使用して、デバイスのプロパティの現在の設定を変更および取得できます。

- ソフトウェアキー

  ドライバーのソフトウェアキーは、各ドライバーのソフトウェアキーがレジストリに格納されているので、その*ドライバーキー*とも呼ばれます。 レジストリには、すべてのデバイスクラスの一覧が含まれており、各ドライバーのソフトウェアキーはそのデバイスクラスエントリに存在します。 システムは、各ドライバーに関する情報をソフトウェアキーの下に保存します。

  ドライバーは[**IWDFPropertyStoreFactory:: RetrieveDevicePropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfpropertystorefactory-retrievedevicepropertystore)を呼び出して、そのソフトウェアキーの値に対する読み取りまたは書き込みアクセス権を取得できます。 ドライバーは、特定のデバイスに関連付けられていないドライバー固有の情報の読み取りと書き込みを行うことができます。

- デバイスインターフェイスキー

  レジストリには、ドライバーによって作成されたすべての[デバイスインターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)のキーが含まれています。 これらの各キーの下には、ドライバーが登録したデバイスインターフェイスクラスの各インスタンスのエントリが含まれます。

  ドライバーがデバイスインターフェイスクラスのインスタンスを登録している場合は、 [**IWDFPropertyStoreFactory:: RetrieveDevicePropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfpropertystorefactory-retrievedevicepropertystore)を呼び出すことによって、そのインスタンスのレジストリエントリの下にある値の読み取りと書き込みを行うことができます。 ドライバーは、デバイスインターフェイスに関するインスタンス固有の情報を読み書きできます。

- **DEVICEMAP**キー

  レジストリには、 **HKEY\_ローカル\_マシン\\ハードウェア\\DEVICEMAP**キーが含まれています。これは、シリアルポートやパラレルポートなど、古いテクノロジの一部のドライバーで使用されることを示しています。 ドライバーが**DEVICEMAP**キーを使用するテクノロジをサポートしている場合、ドライバーは[**IWDFPropertyStoreFactory:: RetrieveDevicePropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfpropertystorefactory-retrievedevicepropertystore)を呼び出すことによって、キーの下のサブキーと値にアクセスできます。

ドライバーが**RetrieveDevicePropertyStore**メソッドのいずれかを呼び出してレジストリサブキーを開くと、ドライバーは[**Iwdfnamedpropertystore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfnamedpropertystore)、 [**IWDFNamedPropertyStore2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfnamedpropertystore2)、または[**IWDFUnifiedPropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfunifiedpropertystore)によって公開されているメソッドを使用できます。サブキーの下に値を作成、読み取り、および書き込みを行います。 **IWDFNamedPropertyStore2**インターフェイスを使用すると、ドライバーは値を削除することもできます。

ドライバーのレジストリキーの詳細については、「[レジストリツリーとキーの概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-registry-trees-and-keys)」を参照してください。

 

 





