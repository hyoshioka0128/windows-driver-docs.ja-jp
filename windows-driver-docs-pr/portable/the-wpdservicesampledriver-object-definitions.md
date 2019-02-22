---
Description: Defining the Service Objects
title: サービス オブジェクトを定義します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 965836fb50baeb873f8f5edee9be2c618fc5cdcd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528289"
---
# <a name="defining-the-service-objects"></a>サービス オブジェクトを定義します。


WPD では、デバイス上の論理エンティティをオブジェクトと呼びます。 オブジェクトは、デバイスの情報や機能の部分を表すことができます。 任意のオブジェクトには、1 つまたは複数のプロパティがあります。 プロパティは、オブジェクトの説明のメタデータとして考えることができます。 たとえば、サンプル ドライバーでアドレス帳サービス オブジェクトは、サービスのフレンドリ名を指定する名前プロパティをサポートします。

WpdHelloWorldDriver には、次の表に示すオブジェクトがサポートしています。

| オブジェクト  | 説明                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| デバイス  | ファームウェアのバージョンや、モデルでは、フレンドリ名などのわかりやすいプロパティを含むルート オブジェクト。 |
| ストレージ | 記憶域容量、ファイル システムの種類では、空きバイト数などのプロパティを公開するオブジェクト。         |
| Folder  | フォルダー名などのプロパティを公開するオブジェクト。                                                             |
| ファイル    | ファイル名と実際のファイルの内容などのプロパティを公開するオブジェクト。                                      |

 

ストレージ オブジェクトをサポートするためには引き続き、WpdServiceSampleDriver を WpdHelloWorldDriver と同様に、します。 ただし、サンプルは、フォルダーまたはファイル (わかりやすくするため) をサポートしていない、ためこれらのオブジェクトが削除され、連絡先に対応する 1 つのオブジェクトに置き換えられます。 次の表は、新しいドライバーがサポートするオブジェクトを一覧表示します。

| オブジェクト   | 説明                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------|
| デバイス   | ファームウェアのバージョンや、モデルでは、フレンドリ名などのわかりやすいプロパティを含むルート オブジェクト。      |
| ストレージ  | 記憶域容量、ファイル システムの種類では、空きバイト数などのプロパティを公開するオブジェクト。              |
| 連絡先 | オブジェクト識別子、永続的な一意 ID (PUID)、名前などのプロパティを格納するサービス オブジェクト。 |

 

WPD、オブジェクトが文字列で識別されます。 デバイス オブジェクトの文字列識別子が定義されている、 *Portabledevice.h*ヘッダー ファイル。

```cpp
#define WPD_DEVICE_OBJECT_ID  L"DEVICE"
```

ストレージ オブジェクトの文字列識別子が定義されている、 *FakeStorage.h*ヘッダー ファイル。

```cpp
#define STORAGE_OBJECT_ID                                 L"123ABC"
#define STORAGE_CAPACITY_VALUE                            1024 * 1024
#define STORAGE_FREE_SPACE_IN_BYTES_VALUE                 STORAGE_CAPACITY_VALUE
#define STORAGE_SERIAL_NUMBER_VALUE                       L"98765432109876-54321098765432"
#define STORAGE_OBJECT_NAME_VALUE                         L"Internal Memory"
#define STORAGE_FILE_SYSTEM_TYPE_VALUE                    L"FAT32"
#define STORAGE_DESCRIPTION_VALUE                         L"Phone Memory Storage System"
#define STORAGE_CONTAINER_FUNCTIONAL_OBJECT_ID            WPD_DEVICE_OBJECT_ID
#define STORAGE_TYPE                                      WPD_STORAGE_TYPE_FIXED_ROM
```

連絡先オブジェクトの文字列識別子が定義されている、 *FakeContactsServiceContent.h*ヘッダー ファイル。

```cpp
#define CONTACTS_SERVICE_OBJECT_ID                        L"789DEF"
#define CONTACTS_SERVICE_PERSISTENT_UNIQUE_ID             L"{95A95EA9-9904-430E-8FF6-70851F208478}"
#define CONTACTS_SERVICE_OBJECT_NAME_VALUE                L"Contacts"
#define CONTACTS_SERVICE_HUMAN_READABLE_NAME              L"Hello World Phone Contacts"
#define CONTACTS_SERVICE_PREFERRED_FORMAT                 WPD_OBJECT_FORMAT_ABSTRACT_CONTACT
#define CONTACTS_SERVICE_VERSION                          L"1.0"

#define NUM_CONTACT_OBJECTS                               10
```

これらのオブジェクト識別子の定数は、機能オブジェクトの取得を処理するためのソース モジュール内のメソッドに渡される (*FakeDevice.cpp*)。 次の抜粋、 **FakeDevice::GetFunctionalObjects**メソッドは、アドレス帳を使用する方法を示しています\_サービス\_オブジェクト\_ID のコレクションを構築するには、関数オブジェクト (がサポートされています。サービス\_で連絡先が定義されている、 *ContactsDeviceService.h*ヘッダー ファイル、サービス オブジェクトの機能のカテゴリを表します)。

```cpp
    // Add CONTACTS_SERVICE_OBJECT_ID to the functional object identifiers collection
    if (hr == S_OK)
    {
        if ((guidFunctionalCategory  == SERVICE_Contacts) ||
            (guidFunctionalCategory  == WPD_FUNCTIONAL_CATEGORY_ALL))
        {
            pv.vt       = VT_LPWSTR;
            pv.pwszVal  = CONTACTS_SERVICE_OBJECT_ID;
            hr = pFunctionalObjects->Add(&pv);
            CHECK_HR(hr, "Failed to add contacts service object ID");
        }
    }
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdServiceSampleDriver サンプル](the-wpdservicesampledriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





