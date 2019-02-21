---
Description: Defining the Service Properties
title: サービスのプロパティを定義します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf751e8e7964db8eaa19a7d680561350d305521c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553527"
---
# <a name="defining-the-service-properties"></a>サービスのプロパティを定義します。


WPD プロパティは、オブジェクトの説明するメタデータです。 このセクションでは、サンプルのドライバーがサポートするプロパティについて説明します。 連絡先のサービス オブジェクトは、14 個のプロパティをサポートしています。個々 の連絡先オブジェクトは 14 個のプロパティもサポートします。 一部のオブジェクト プロパティに WPD などのドライバーの機能に必要な\_オブジェクト\_ID と WPD\_オブジェクト\_持続\_UNIQUE\_id。 その他のプロパティが WPD など、オブジェクトを記述する情報を提供\_にお問い合わせください\_表示\_連絡先オブジェクトの名前。

WDK には、WPD ドライバー開発者向けのいくつかのツールが含まれています。 これらのツールの 1 つ*WpdInfo.exe*開発者がオブジェクトと特定のドライバーによって公開されているプロパティを確認するに使用します。 次の図の*WpdInfo.exe*ツールは、ドライバーでアドレス帳サービス オブジェクトをサポートするプロパティを示します。

![wpd 情報ツール](images/wpd_info_service_root.png)

前の画像では、上部のウィンドウの左端の列は、ドライバーがサポートするオブジェクトの一覧を表示します。 中央のウィンドウには、アドレス帳のサービス オブジェクトのドライバーがサポートする 14 個のプロパティが一覧表示します。 このペインの最初の列には、プロパティ名が一覧表示されます、2 番目の列が、そのプロパティの値を一覧表示および 3 番目の列には、型、および具合が一覧表示されます。 下のウィンドウには、ドライバーをサポートしているイベントによって返される情報が表示されます。

次の図の*WpdInfo.exe*ツールは、最初の連絡先オブジェクトをサポートしているプロパティを示します。

![wpd 情報ツール](images/wpd_info_service_contact1.png)

このオブジェクトは、14 個のプロパティをサポートします。 最初の 8 プロパティは、一般的な WPD オブジェクトのプロパティです。 過去 6 回のプロパティは、連絡先固有 (名前、携帯電話番号、電子メール アドレス、およびなど)。

WPD では、プロパティが PROPERTYKEY データ構造体によって表されます。 この構造は、2 つの部分で構成されます。 グローバル一意識別子 (GUID) と DWORD。 GUID がプロパティのカテゴリを識別し、dword 値がそのカテゴリ内の特定のプロパティを識別します。 PROPERTYKEY 構造の詳細については、次を参照してください。 [PROPERTYKEYs と WPD で Guid](propertykeys-and-guids-in-windows-portable-devices.md)します。

配列で、サンプル ドライバーでサポートされている連絡先のプロパティが定義されている**PropertyAttributeInfo**構造体。 この構造体には、次の形式があります。

```cpp
typedef struct tagPropertyAttributeInfo
{
    const PROPERTYKEY*                pKey;
    VARTYPE                           Vartype;
    FakeDevicePropertyAttributesType  AttributesType;
    const LPWSTR                      wszName;
} PropertyAttributeInfo;
```

*FakeContactContent.cpp*ファイルがサポートされている連絡先プロパティの配列を定義します。

```cpp
const PropertyAttributeInfo g_SupportedContactProperties[] =
{
    {&WPD_OBJECT_ID,                             VT_LPWSTR, UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast,  NULL}, 
    {&WPD_OBJECT_PERSISTENT_UNIQUE_ID,           VT_LPWSTR, UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast,  NULL}, 
    {&WPD_OBJECT_PARENT_ID,                      VT_LPWSTR, UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast,  NULL}, 
    {&WPD_OBJECT_NAME,                           VT_LPWSTR, UnspecifiedForm_CanRead_CanWrite_CannotDelete_Fast,     NULL}, 
    {&WPD_OBJECT_FORMAT,                         VT_CLSID,  UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast,  NULL}, 
    {&WPD_OBJECT_CONTENT_TYPE,                   VT_CLSID,  UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast,  NULL}, 
    {&WPD_OBJECT_CAN_DELETE,                     VT_BOOL,   UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast,  NULL}, 
    {&WPD_OBJECT_CONTAINER_FUNCTIONAL_OBJECT_ID, VT_LPWSTR, UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast,  NULL}, 
    {&WPD_CONTACT_DISPLAY_NAME,                  VT_LPWSTR, UnspecifiedForm_CanRead_CanWrite_CannotDelete_Fast,     NULL},
    {&WPD_CONTACT_MOBILE_PHONE,                  VT_LPWSTR, UnspecifiedForm_CanRead_CanWrite_CannotDelete_Fast,     NULL},
    {&WPD_CONTACT_PRIMARY_EMAIL_ADDRESS,         VT_LPWSTR, UnspecifiedForm_CanRead_CanWrite_CannotDelete_Fast,     NULL},
    {&WPD_CONTACT_PRIMARY_PHONE,                 VT_LPWSTR, UnspecifiedForm_CanRead_CanWrite_CannotDelete_Fast,     NULL},
    {&WPD_CONTACT_PERSONAL_FULL_POSTAL_ADDRESS,  VT_LPWSTR, UnspecifiedForm_CanRead_CanWrite_CannotDelete_Fast,     NULL},
    {&MyContactVersionIdentifier,                VT_UI4,    UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast,  L"ContactVersionIdentifier"},
};
```

これらのプロパティが初期化されます、 *FakeContactsServiceContent.cpp*でモジュール、 **InitializeContent**メソッドを次の例に示すようにします。

```cpp
        if (pContact)
        {
            pContact->Name.Format(L"Contact%d", *pdwLastObjectID);
            pContact->ParentID                    = ObjectID;
            pContact->ContainerFunctionalObjectID = ObjectID;
            pContact->ObjectID.Format(L"%d", *pdwLastObjectID);
            pContact->PersistentUniqueID.Format(L"PersistentUniqueID_%ws", pContact->ObjectID);
            pContact->ParentPersistentUniqueID    = PersistentUniqueID;
            pContact->RequiredScope               = CONTACTS_SERVICE_ACCESS;

            pContact->DisplayName.Format(L"Surname%d, FirstName%d", dwContactIndex, dwContactIndex);
            pContact->MobilePhoneNumber           = L"(425) 555 0821";
            pContact->PrimaryPhoneNumber          = L"(425) 556 6010";
            pContact->PrimaryEmail.Format(L"FirstName%d@Company%d.com", dwContactIndex, dwContactIndex);
            pContact->PersonalFullPostalAddress.Format(L"One Microsoft Way, Redmond, WA 98052, USA");

            m_Children.Add(pContact);
        }
```

*FakeContactsServiceContent.cpp*ファイルがサポートされているサービスのプロパティの配列を定義します。

```cpp
const PropertyAttributeInfo g_SupportedServiceProperties[] =
{
    {&WPD_OBJECT_ID,                                VT_LPWSTR,          UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, NULL},
    {&WPD_OBJECT_PERSISTENT_UNIQUE_ID,              VT_LPWSTR,          UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, NULL},
    {&WPD_OBJECT_PARENT_ID,                         VT_LPWSTR,          UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, NULL},
    {&WPD_OBJECT_NAME,                              VT_LPWSTR,          UnspecifiedForm_CanRead_CanWrite_CannotDelete_Fast,    NULL},
    {&WPD_OBJECT_FORMAT,                            VT_CLSID,           UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, NULL},
    {&WPD_OBJECT_CONTENT_TYPE,                      VT_CLSID,           UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, NULL},
    {&WPD_OBJECT_CAN_DELETE,                        VT_BOOL,            UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, NULL},
    {&WPD_OBJECT_CONTAINER_FUNCTIONAL_OBJECT_ID,    VT_LPWSTR,          UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, NULL},
    {&WPD_FUNCTIONAL_OBJECT_CATEGORY,               VT_CLSID,           UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, NULL},
    {&WPD_SERVICE_VERSION,                          VT_LPWSTR,          UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, NULL},
    {&PKEY_Services_ServiceDisplayName,             VT_LPWSTR,          UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, L"DisplayName"},
    {&PKEY_FullEnumSyncSvc_SyncFormat,              VT_CLSID,           UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, L"FullEnumSyncFormat"},
    {&PKEY_Services_ServiceIcon,                    VT_VECTOR | VT_UI1, UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, L"ServiceIcon"},
    {&PKEY_FullEnumSyncSvc_VersionProps,            VT_VECTOR | VT_UI1, UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, L"FullEnumVersionProps"}
};
```

サービスのプロパティが設定されて、 **GetValue**同じモジュールに含まれるメソッド。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdServiceSampleDriverSample](the-wpdservicesampledriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





