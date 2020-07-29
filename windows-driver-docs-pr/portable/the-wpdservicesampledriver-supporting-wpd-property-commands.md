---
Description: プロパティコマンドを使用したスコープアクセスの使用 (Wpdサービス Amwadriver)
title: プロパティコマンドを使用したスコープアクセスの使用 (Wpdサービス Amwadriver)
ms.date: 07/27/2020
ms.localizationpriority: medium
ms.openlocfilehash: e77c4b744bf0c61ede97742fdd55573bd8ffc3e3
ms.sourcegitcommit: 9102e34c3322d8697dbb6f9a1d78879147a73373
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264441"
---
# <a name="using-scope-access-with-property-commands-wpdservicesampledriver"></a>プロパティコマンドを使用したスコープアクセスの使用 (Wpdサービス Amwadriver)


サンプルドライバーでは、6つのプロパティコマンドがサポートされています。 これらのコマンドは、最初に**WpdObjectProperties::D ispatchmessage**メソッドによって処理され、次に対応するコマンドハンドラーが呼び出されます。 **DispatchMessage**メソッドと個々のハンドラーはすべて、 *WpdObjectProperties ファイル*に含まれています。

次の表では、サポートされている各プロパティコマンドと、特定のコマンドを処理するときに**DispatchMessage**が呼び出すハンドラーの名前について説明します。

| command                                           | Handler                  | 説明                                                                                                   |
|---------------------------------------------------|--------------------------|---------------------------------------------------------------------------------------------------------------|
| WPD \_ コマンド \_ オブジェクトの \_ プロパティが \_ \_ サポートされています  | OnGetSupportedProperties | 指定されたオブジェクトのプロパティキーの配列を返します。                                                       |
| WPD \_ コマンド \_ オブジェクトの \_ プロパティ \_ 取得             | OnGetPropertyValues      | ドライバーに渡されたプロパティキーに対応するプロパティ値のコレクションを返します。 |
| WPD \_ コマンド \_ オブジェクトの \_ プロパティを \_ \_ すべて取得        | OnGetAllProperties       | 指定されたオブジェクトのすべてのプロパティ値を返します。                                                           |
| WPD \_ コマンド \_ オブジェクトの \_ プロパティの \_ 設定             | OnSetPropertyValues      | デバイスで指定されたプロパティ値を設定します。                                                              |
| WPD \_ コマンド \_ オブジェクト \_ プロパティ \_ の \_ 属性の取得 | OnGetPropertyAttributes  | 指定されたオブジェクトの1つ以上のプロパティの属性のコレクションを返します。                              |
| WPD \_ コマンド \_ オブジェクトの \_ プロパティの \_ 削除          | OnDeleteProperties       | 指定されたプロパティキーによって識別されるプロパティを削除します。                                        |



## <a name="span-idusing_access_scope_when_setting_and_retrieving_properties_spanspan-idusing_access_scope_when_setting_and_retrieving_properties_spanspan-idusing_access_scope_when_setting_and_retrieving_properties_spanusing-access-scope-when-setting-and-retrieving-properties"></a><span id="Using_Access_Scope_when_Setting_and_Retrieving_Properties_"></span><span id="using_access_scope_when_setting_and_retrieving_properties_"></span><span id="USING_ACCESS_SCOPE_WHEN_SETTING_AND_RETRIEVING_PROPERTIES_"></span>プロパティの設定および取得時にアクセススコープを使用する


Wpdの Am氏ドライバーの6つのプロパティハンドラーにあるコードは、WpdHelloWorld ドライバーに含まれるコードとほぼ同じです。 この例外は、Windows 7 の新しい概念である*サービスレベルのアクセススコープ*です。

サービスレベルのアクセススコープを使用すると、ドライバーは、特定の親サービスで検出されたオブジェクトのみに列挙を制限できます。 ドライバーがアクセススコープをサポートしていて、アプリケーションが**Iportabledeviceservice:: Open**メソッドを (特定のサービスのプラグアンドプレイ識別子を渡して) 呼び出す場合、アプリケーションは、そのサービスのデバイス、指定されたサービス、および子オブジェクトにのみアクセスできます。 アクセススコープの実装は、ドライバーによって異なる場合があります。 Wpdservices Amwadriver は、ビットマスクを使用して、2つの基本レベルのスコープ、デバイスレベル (制限の緩い)、およびサービスレベル (より制限の厳しい) を定義することで、この概念を示しています。 次のコード例は、これらのレベルの違いを示しています。

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

ドライバーが列挙ツリーにフェイクオブジェクトを設定すると、各コンテンツオブジェクトの**Fakecontent:: RequiredScope**メンバーが適切なスコープで初期化されます。 たとえば、Contacts オブジェクトを初期化して、サービスレベルのアクセスのみに制限することができます。

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

次の**OnGetSupportedProperties** handler 関数のコード例は、正しいプロパティキーが返されたことを確認するためにアクセススコープがどのように使用されたかを示しています。

```ManagedCPlusPlus
    // Add supported property keys for the specified object to the collection
    if (hr == S_OK)
    {
        ACCESS_SCOPE Scope = m_pDevice->GetAccessScope(pParams);
        hr = m_pDevice->GetSupportedProperties(Scope, wszObjectID, pKeys);
        CHECK_HR(hr, "Failed to add supported property keys for object '%ws'", wszObjectID);
    }
```

前の例のコードでは、 **fakedevice:: GetSupportedProperties**メソッドを呼び出しています。このメソッドは、ファイル*fakedevice .cpp*にあります。

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

このメソッドは、まず、指定されたオブジェクトのコンテンツを取得しようとします。 次に、メソッドがコンテンツを取得できる場合は、要求されたプロパティキーを取得します。**Fakecontent::** は、スコープを確認し、アプリケーションが制限の緩いアクセススコープ (デバイス全体のアクセスなど) を提供する場合にアクセスを拒否します。

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

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[Wpdbasicハードウェアのサンプル](the-wpdbasichardwaredriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)









