---
Description: プロパティ コマンド (WpdBasicHardwareDriverSample) のサポート
title: プロパティ コマンド (WpdBasicHardwareDriverSample) のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd89ce3ce9653958bf77bc3c2c0d8d6f45c897ad
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349691"
---
# <a name="support-for-property-commands-wpdbasichardwaredriversample"></a>プロパティ コマンド (WpdBasicHardwareDriverSample) のサポート


ドライバーのサンプルでは、6 つのプロパティのコマンドをサポートします。 これらのコマンドが最初に、処理、 **WpdObjectProperties::DispatchMessage**メソッドを対応するコマンド ハンドラーが呼び出されます。 **DispatchMessage**メソッドと個別のハンドラーは、すべてで、 *WpdObjectProperties.cpp ファイル*します。

次の表では、ハンドラーの名前と共に、サポートされているプロパティのコマンドのそれぞれについて説明しますが**DispatchMessage**特定のコマンドを処理するときに呼び出します。

| コマンド                                           | ハンドラー                  | 説明                                                                                                   |
|---------------------------------------------------|--------------------------|---------------------------------------------------------------------------------------------------------------|
| WPD\_コマンド\_オブジェクト\_プロパティ\_取得\_サポートされています。  | OnGetSupportedProperties | 指定したオブジェクトのプロパティのキーの配列を返します。                                                       |
| WPD\_コマンド\_オブジェクト\_プロパティ\_取得             | OnGetPropertyValues      | ドライバーに渡されるプロパティのキーに対応するプロパティ値のコレクションを返します。 |
| WPD\_コマンド\_オブジェクト\_プロパティ\_取得\_すべて        | OnGetAllProperties       | 指定したオブジェクトのすべてのプロパティ値を返します。                                                           |
| WPD\_コマンド\_オブジェクト\_プロパティ\_設定             | OnSetPropertyValues      | デバイスでは、指定されたプロパティ値を設定します。                                                              |
| WPD\_コマンド\_オブジェクト\_プロパティ\_取得\_属性 | OnGetPropertyAttributes  | 指定したオブジェクトでは、1 つまたは複数のプロパティの属性のコレクションを返します。                              |
| WPD\_コマンド\_オブジェクト\_プロパティ\_削除          | OnDeleteProperties       | 指定したプロパティのキーによって識別されるプロパティを削除します。                                        |



## <a name="span-idusingaccessscopewhensettingandretrievingpropertiesspanspan-idusingaccessscopewhensettingandretrievingpropertiesspanspan-idusingaccessscopewhensettingandretrievingpropertiesspanusing-access-scope-when-setting-and-retrieving-properties"></a><span id="Using_Access_Scope_when_Setting_and_Retrieving_Properties_"></span><span id="using_access_scope_when_setting_and_retrieving_properties_"></span><span id="USING_ACCESS_SCOPE_WHEN_SETTING_AND_RETRIEVING_PROPERTIES_"></span>設定するときに、アクセス スコープを使用して、プロパティを取得します。


WpdServiceSampleDriver で 6 つのプロパティのハンドラーに含まれるコードは、WpdHelloWorld ドライバーに含まれるコードとほぼ同じです。 例外は*サービス レベルのアクセス スコープ*Windows 7 の新しい概念であります。

サービス レベルのアクセス スコープ列挙を指定した親サービスの下にあるオブジェクトのみを制限するためのドライバーを使用できます。 ドライバーは、アクセス スコープをサポートしているし、アプリケーションが呼び出す、 **IPortableDeviceService::Open**メソッド (を渡すことによって、特定のサービスのプラグ アンド プレイ識別子)、アプリケーションのみがアクセスできる、デバイスでは、特定のサービスそのサービスの子オブジェクト。 アクセス スコープの実装は、ドライバーによって異なる場合があります。 WpdServiceSampleDriver スコープ、(より制限の少ない)、デバイス レベルの 2 つの基本的なレベルを定義するビットマスクを使用して、この概念を示していて、サービス レベル (より制限の厳しい)。 次のコード例では、これらのレベルの違いを示します。

```ManagedCPlusPlus
// Access Scope is a bit mask, where each bit enables access to a particular scope
// for example, contacts service is bit 1.   
// The next scope, if any, will be in bit 2
// Full device access is a combination of all, requires all bits to be set
typedef enum tagACCESS_SCOPE
{
    CONTACTS_SERVICE_ACCESS = 1,
    FULL_DEVICE_ACCESS = 0xFFFFFFFF
}ACCESS_SCOPE;
```

ドライバーとフェイク オブジェクトは、列挙型のツリーを設定するときに、 **FakeContent::RequiredScope**各コンテンツ オブジェクトのメンバーは、適切なスコープで初期化されます。 たとえば、アドレス帳サービス レベルのアクセスのみに制限されている連絡先オブジェクトを初期化できます。

```ManagedCPlusPlus
class FakeContactContent : public FakeContent
{
public:
    FakeContactContent()
    {
        Format              = WPD_OBJECT_FORMAT_ABSTRACT_CONTACT;
        ContentType         = WPD_CONTENT_TYPE_CONTACT;
        RequiredScope       = CONTACTS_SERVICE_ACCESS;
    ...
    }
  ...
}
```

次のコード例から、 **OnGetSupportedProperties**ハンドラー関数が適切なプロパティのキーが返されたことを確認するアクセス スコープの使用方法を示しています。

```ManagedCPlusPlus
    // Add supported property keys for the specified object to the collection
    if (hr == S_OK)
    {
        ACCESS_SCOPE Scope = m_pDevice->GetAccessScope(pParams);
        hr = m_pDevice->GetSupportedProperties(Scope, wszObjectID, pKeys);
        CHECK_HR(hr, "Failed to add supported property keys for object '%ws'", wszObjectID);
    }
```

コードで、前の例では、 **FakeDevice::GetSupportedProperties**メソッドは、ファイルにある*FakeDevice.cpp*します。

```ManagedCPlusPlus
HRESULT FakeDevice::GetSupportedProperties(
            ACCESS_SCOPE                  Scope,
    __in    LPCWSTR                       wszObjectID,
    __out   IPortableDeviceKeyCollection* pKeys)
{
    HRESULT      hr       = S_OK;
    FakeContent* pContent = NULL;

    if ((wszObjectID == NULL) ||
        (pKeys       == NULL))
    {
        hr = E_POINTER;
        CHECK_HR(hr, "Cannot have NULL parameter");
        return hr;
    }

    hr = GetContent(Scope, wszObjectID, &pContent);
    CHECK_HR(hr, "Failed to get content '%ws'", wszObjectID);

    if (hr == S_OK)
    {
        hr = pContent->GetSupportedProperties(pKeys);
        CHECK_HR(hr, "Failed to get supported properties for '%ws'", wszObjectID);
    }

    return hr;
}
```

このメソッドは、最初に、指定したオブジェクトの内容を取得しようとします。 次に、メソッドが、コンテンツを取得できない場合は、要求されたプロパティのキーを取得します。**FakeContent::GetContent**スコープを確認し、アプリケーションがデバイス全体にわたるアクセス) などの緩いアクセス スコープを提供する場合は、アクセスを拒否します。

```ManagedCPlusPlus
HRESULT FakeContent::GetContent(
            ACCESS_SCOPE   Scope,
    __in    LPCWSTR        wszObjectID,
    __out   FakeContent**  ppContent)
{
    HRESULT hr = HRESULT_FROM_WIN32(ERROR_NOT_FOUND);

    if (CanAccess(Scope))
    {
    // Within access scope, proceed . . .
    }
    else
    {
        hr = E_ACCESSDENIED;
        CHECK_HR(hr, "GetContent: '%ws' was found but falls outside scope", wszObjectID);
    }

    return hr;
} 

bool FakeContent::CanAccess(
    ACCESS_SCOPE Scope)
{
    return ((Scope & RequiredScope) == RequiredScope);
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)









