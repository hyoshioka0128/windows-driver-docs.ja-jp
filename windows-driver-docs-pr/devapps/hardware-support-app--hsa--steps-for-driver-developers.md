---
title: ドライバー開発者向けのハードウェアサポートアプリ (HSA) の手順
description: ドライバーとハードウェアサポートアプリをペアリングするカスタム機能の作成 (HSA)
keywords:
- カスタム、機能
- UWP アプリ
- カスタム機能
- UWP
- ハードウェア
ms.date: 08/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c18ff9030cd7dcdc95e747e8736a641016d1a793
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235424"
---
# <a name="hardware-support-app-hsa-steps-for-driver-developers"></a>ハードウェアサポートアプリ (HSA): ドライバー開発者向けの手順

ハードウェアサポートアプリ (HSA) は、特定のドライバーまたは[RPC (リモートプロシージャコール)](https://docs.microsoft.com/windows/desktop/Rpc/rpc-start-page)エンドポイントとペアになっているデバイス固有のアプリです。

ストアアプリをドライバーに関連付けるには、まず、カスタム機能と呼ばれる特別な値を予約します。 次に、機能を提供するアプリへのアクセスを許可し、アプリの開発者に機能を提供します。  このページでは、ドライバーの開発者向けの手順について説明します。

アプリ開発者向けの手順については、「[ハードウェアサポートアプリ (HSA): アプリ開発者向けの手順](hardware-support-app--hsa--steps-for-app-developers.md)」を参照してください。

HSA は、 [Windows ドライバー](../develop/getting-started-with-windows-drivers.md)の3つの ("dch") 設計原則の1つです。

## <a name="reserving-a-custom-capability"></a>カスタム機能の予約

まず、カスタム機能を予約します。

1.  Microsoft ハードウェアサポートアプリのレビュー ( <HSAReview@microsoft.com> ) について、次の情報を電子メールでお読みください。

    * 連絡先情報
    * 会社名
    * 機能の名前 (一意であり、所有者を参照する必要があります)
    * 機能にはどのようなリソースにアクセスする必要がありますか。
    * セキュリティまたはプライバシーの問題
    * どのようなデータイベントがパートナーに処理されますか。
      * イベントには、正確なユーザーの場所、パスワード、IP アドレス、PUID、デバイス ID、CID、ユーザー名、連絡先データなどの個人識別子が含まれますか。
      * データイベントはユーザーのデバイスにとどまりますか、それともパートナーに送信されますか?
    * 機能によってどのようなデータにアクセスできるか。
    * この機能のエンドユーザーにはどのような利点がありますか。
    * Microsoft Store アプリの発行元 ID を含めます。  1つを取得するには、[Microsoft Store] ページでスケルトンアプリエントリを作成します。 アプリの PFN を予約する方法の詳細については、「[名前を予約してアプリを作成](https://docs.microsoft.com/windows/uwp/publish/create-your-app-by-reserving-a-name)する」を参照してください。

2.  要求が承認された場合、Microsoft は、 **capabilityName \_ PublisherID**の形式で一意のカスタム機能文字列名を返します。

これで、カスタム機能を使用して、RPC エンドポイントまたはドライバーへのアクセスを許可できるようになりました。

## <a name="allowing-access-to-an-rpc-endpoint-to-a-uwp-app-using-the-custom-capability"></a>カスタム機能を使用して UWP アプリへの RPC エンドポイントへのアクセスを許可する

カスタム機能を持つ UWP アプリへの RPC エンドポイントへのアクセスを許可するには、次の手順を実行します。

1.  [**DeriveCapabilitySidsFromName**](https://docs.microsoft.com/windows/desktop/api/securitybaseapi/nf-securitybaseapi-derivecapabilitysidsfromname)を呼び出して、カスタム機能名をセキュリティ ID (SID) に変換します。
2.  アクセスが許可されている ACE に SID を追加し、RPC エンドポイントのセキュリティ記述子に必要なその他の Sid を追加します。
3.  セキュリティ記述子の情報を使用して RPC エンドポイントを作成します。

上記の実装については、「[カスタム機能のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CustomCapability)」の[RPC サーバーコード](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/CustomCapability/Service/Server/RpcServer.cpp)を参照してください。

## <a name="allowing-access-to-a-driver-to-a-uwp-app-using-the-custom-capability"></a>カスタム機能を使用して UWP アプリへのドライバーのアクセスを許可する

カスタム機能を備えた UWP アプリへのドライバーのアクセスを許可するには、INF ファイルまたはドライバーソースのいずれかに数行を追加します。

INF ファイルで、次のようにカスタム機能を指定します。

```cpp
[WDMPNPB003_Device.NT.Interfaces] 
AddInterface= {zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz},,AddInterfaceSection 
 
[AddInterfaceSection] 
AddProperty= AddInterfaceSection.AddProps 
 
[AddInterfaceSection.AddProps] 
; DEVPKEY_DeviceInterface_UnrestrictedAppCapabilities 
{026e516e-b814-414b-83cd-856d6fef4822}, 8, 0x2012,, "CompanyName.myCustomCapabilityNameTBD_MyStorePubId"
```

または、ドライバーで次の操作を実行します。

```c++
WDF_DEVICE_INTERFACE_PROPERTY_DATA PropertyData = {}; 
WCHAR customCapabilities[] = L”CompanyName.myCustomCapabilityNameTBD_MyStorePubId\0”; 
 
WDF_DEVICE_INTERFACE_PROPERTY_DATA_INIT( 
   &PropertyData, 
   &m_VendorDefinedSubType, 
   &DEVPKEY_DeviceInterface_UnrestrictedAppCapabilities); 
 
Status = WdfDeviceAssignInterfaceProperty( 
    m_FxDevice, 
    &PropertyData, 
    DEVPROP_TYPE_STRING_LIST, 
    ARRAYSIZE(customCapabilities), 
    reinterpret_cast<PVOID>(customCapabilities)); 

```

`zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz`を公開するインターフェイスの GUID で置き換えます。  *CompanyName*を会社名、 *myCustomCapabilityNameTBD*を会社内で一意の名前に、 *mystorepubid*を発行元ストア ID に置き換えます。 

上に示したドライバーコードの例については、「[ドライバーパッケージインストールツールキット (ユニバーサルドライバー用](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU))」を参照してください。

## <a name="preparing-the-signed-custom-capability-descriptor-sccd-file"></a>署名されたカスタム機能記述子 (SCCD) ファイルを準備しています

署名されたカスタム機能記述子 (SCCD) ファイルは、1つまたは複数のカスタム機能の使用を承認する署名付き XML ファイルです。  ドライバーまたは RPC エンドポイントの所有者は、このファイルを提供することで、アプリ開発者にカスタム機能を付与します。

SCCD ファイルを準備するには、まず、カスタム機能文字列を更新します。  次の例を出発点として使用します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<CustomCapabilityDescriptor xmlns="http://schemas.microsoft.com/appx/2016/sccd" xmlns:s="http://schemas.microsoft.com/appx/2016/sccd">
<CustomCapabilities>
    <CustomCapability Name="microsoft.hsaTestCustomCapability_q536wpkpf5cy2"></CustomCapability>
</CustomCapabilities>
<AuthorizedEntities>
    <AuthorizedEntity AppPackageFamilyName="MicrosoftHSATest.Microsoft.SDKSamples.Hsa.CPP_q536wpkpf5cy2" CertificateSignatureHash="ca9fc964db7e0c2938778f4559946833e7a8cfde0f3eaa07650766d4764e86c4"></AuthorizedEntity>
</AuthorizedEntities>
<Catalog>0000</Catalog>
</CustomCapabilityDescriptor>
```

次に、カスタム機能の所有者は、アプリ開発者からパッケージファミリ名 (PFN) と署名ハッシュを取得し、SCCD ファイル内のこれらの文字列を更新します。

**注:** アプリは証明書を使用して直接署名する必要はありませんが、指定された証明書は、アプリに署名する証明書チェーンの一部である必要があります。

SCCD が完了すると、機能所有者は署名のために Microsoft に電子メールを受け取ります。  Microsoft は、署名された SCCD を機能所有者に返します。

次に、機能所有者が SCCD をアプリ開発者に送信します。  アプリの開発者は、署名された SCCD をアプリケーションマニフェストに含めます。  アプリ開発者が行う必要がある操作については、「[ハードウェアサポートアプリ (HSA): アプリ開発者向けの手順](hardware-support-app--hsa--steps-for-app-developers.md)」を参照してください。

## <a name="limiting-the-scope-of-an-sccd"></a>SCCD のスコープを制限する

テストを目的として、カスタム機能の所有者は、ハードウェアサポートアプリのインストールを開発者モードのコンピューターに制限することができます。

これを行うには、Microsoft によって署名された SCCD を取得する前に、 **DeveloperModeOnly**を追加します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<CustomCapabilityDescriptor xmlns="http://schemas.microsoft.com/appx/2016/sccd" xmlns:s="http://schemas.microsoft.com/appx/2016/sccd">
<CustomCapabilities>
    <CustomCapability Name="microsoft.hsaTestCustomCapability_q536wpkpf5cy2"></CustomCapability>
</CustomCapabilities>
<AuthorizedEntities>
    <AuthorizedEntity AppPackageFamilyName="MicrosoftHSATest.Microsoft.SDKSamples.Hsa.CPP_q536wpkpf5cy2" CertificateSignatureHash="ca9fc964db7e0c2938778f4559946833e7a8cfde0f3eaa07650766d4764e86c4"></AuthorizedEntity>
</AuthorizedEntities>
<Catalog>0000</Catalog>
<DeveloperModeOnly Value="true" />
</CustomCapabilityDescriptor>
```

生成された署名付き SCCD は、[開発者モード](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)のデバイスでのみ動作します。 

## <a name="allowing-any-app-to-use-a-custom-capability"></a>すべてのアプリにカスタム機能の使用を許可する

カスタム機能を使用できる承認済みエンティティ (アプリ) を指定することをお勧めします。 ただし、場合によっては、すべてのアプリに SCCD を含めることを許可する必要があります。  Windows 10 バージョン1809以降では、 **Allowany**を AuthorizedEntities 要素に追加することによってこれを行うことができます。 ベストプラクティスとして、SCCD ファイルで承認済みエンティティを宣言することをお勧めします。 Microsoft によって署名されるように SCCD を送信する場合は、 **Allowany**を使用する理由を指定してください。

```xml
<?xml version="1.0" encoding="utf-8"?>
<CustomCapabilityDescriptor xmlns="http://schemas.microsoft.com/appx/2018/sccd" xmlns:s="http://schemas.microsoft.com/appx/2018/sccd">
<CustomCapabilities>
    <CustomCapability Name="microsoft.hsaTestCustomCapability_q536wpkpf5cy2"></CustomCapability>
</CustomCapabilities>
<AuthorizedEntities AllowAny="true"/>
<Catalog>0000</Catalog>
</CustomCapabilityDescriptor>
```

結果として得られる署名付き SCCD は、任意のアプリケーションパッケージで検証します。 

## <a name="multiple-sccds"></a>複数の SCCDs

Windows 10 バージョン1803以降では、アプリは1つ以上の SCCD ファイルからカスタム機能を宣言できます。 SCCD ファイルをアプリケーションパッケージのルートに配置します。

## <a name="summary"></a>まとめ

次の図は、上で説明したシーケンスの概要を示しています。

![SCCD 署名を取得する](images/signsccd.png)

## <a name="see-also"></a>参照

* [Windows ドライバーでのはじめに](../develop/getting-started-with-windows-drivers.md)
* [ユニバーサル Windows プラットフォームの紹介](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide)
* [ユニバーサル Windows プラットフォーム (UWP)](https://docs.microsoft.com/windows/uwp/design/basics/design-and-ui-intro)
* [アプリの機能](https://docs.microsoft.com/windows/uwp/packaging/app-capability-declarations)
* [Visual Studio を使用して UWP アプリを開発する](https://docs.microsoft.com/windows/uwp/develop/)
* [ドライバーとユニバーサル Windows プラットフォーム (UWP) アプリとのペアリング](../install/pairing-app-and-driver-versions.md)
* [UWP アプリを開発する](https://docs.microsoft.com/windows/uwp/develop/)
* [Desktop App Converter を使用してアプリをパッケージ化する (デスクトップ ブリッジ)](https://docs.microsoft.com/windows/uwp/porting/desktop-to-uwp-run-desktop-app-converter)
* [カスタム機能のサンプルアプリ](https://go.microsoft.com/fwlink/p/?LinkId=846904)
* [カスタム機能ドライバーのサンプル](https://aka.ms/customcapabilitydriversample )
* [Windows 10 でのアプリのサイドローディング](https://docs.microsoft.com/windows/deploy/sideload-apps-in-windows-10)
* [カスタム機能に関する FAQ](FAQ-on-custom-capabilities.md)

## <a name="sccd-xml-schema"></a>SCCD XML スキーマ

SCCD ファイルの正式な XML XSD スキーマを次に示します。  このスキーマを使用して、確認のために送信する前に SCCD を検証します。  スキーマのインポートと IntelliSense による検証の詳細については、「[スキーマキャッシュ](https://docs.microsoft.com/visualstudio/xml-tools/schema-cache)と[XML ドキュメントの検証](https://docs.microsoft.com/visualstudio/xml-tools/xml-document-validation)」を参照してください。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified"
  xmlns:xs="http://www.w3.org/2001/XMLSchema"
  targetNamespace="http://schemas.microsoft.com/appx/2016/sccd"
  xmlns:s="http://schemas.microsoft.com/appx/2016/sccd"
  xmlns="http://schemas.microsoft.com/appx/2016/sccd">

  <xs:element name="CustomCapabilityDescriptor" type="CT_CustomCapabilityDescriptor">
    <xs:unique name="Unique_CustomCapability_Name">
      <xs:selector xpath="s:CustomCapabilities/s:CustomCapability"/>
      <xs:field xpath="@Name"/>
    </xs:unique>
  </xs:element>

  <xs:complexType name="CT_CustomCapabilityDescriptor">
    <xs:sequence>
      <xs:element ref="CustomCapabilities" minOccurs="1" maxOccurs="1"/>
      <xs:element ref="AuthorizedEntities" minOccurs="1" maxOccurs="1"/>
      <xs:element ref="DeveloperModeOnly" minOccurs="0" maxOccurs="1"/>
      <xs:element ref="Catalog" minOccurs="1" maxOccurs="1"/>
      <xs:any minOccurs="0"/>
    </xs:sequence>
  </xs:complexType>

  <xs:element name="CustomCapabilities" type="CT_CustomCapabilities" />

  <xs:complexType name="CT_CustomCapabilities">
    <xs:sequence>
      <xs:element ref="CustomCapability" minOccurs="1" maxOccurs="unbounded"/>
    </xs:sequence>
  </xs:complexType>

  <xs:element name="CustomCapability">
    <xs:complexType>
      <xs:attribute name="Name" type="ST_CustomCapability" use="required"/>
    </xs:complexType>
  </xs:element>

  <xs:simpleType name="ST_NonEmptyString">
    <xs:restriction base="xs:string">
      <xs:minLength value="1"/>
      <xs:maxLength value="32767"/>
      <xs:pattern value="[^\s]|([^\s].*[^\s])"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:simpleType name="ST_CustomCapability">
    <xs:annotation>
      <xs:documentation>Custom capabilities should be a string in the form of Company.capabilityName_PublisherId</xs:documentation>
    </xs:annotation>
    <xs:restriction base="ST_NonEmptyString">
      <xs:pattern value="[A-Za-z0-9][-_.A-Za-z0-9]*_[a-hjkmnp-z0-9]{13}"/>
      <xs:minLength value="15"/>
      <xs:maxLength value="255"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:element name="AuthorizedEntities" type="CT_AuthorizedEntities" />

  <xs:complexType name="CT_AuthorizedEntities">
    <xs:sequence>
      <xs:element ref="AuthorizedEntity" minOccurs="1" maxOccurs="unbounded"/>
    </xs:sequence>
  </xs:complexType>

  <xs:element name="AuthorizedEntity" type="CT_AuthorizedEntity" />

  <xs:complexType name="CT_AuthorizedEntity">
    <xs:attribute name="CertificateSignatureHash" type="ST_CertificateSignatureHash" use="required"/>
    <xs:attribute name="AppPackageFamilyName" type="ST_NonEmptyString" use="required"/>
  </xs:complexType>

  <xs:simpleType name="ST_CertificateSignatureHash">
    <xs:restriction base="ST_NonEmptyString">
      <xs:pattern value="[A-Fa-f0-9]+"/>
      <xs:minLength value="64"/>
      <xs:maxLength value="64"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:element name="DeveloperModeOnly">
    <xs:complexType>
      <xs:attribute name="Value" type="xs:boolean" use="required"/>
    </xs:complexType>
  </xs:element>

  <xs:element name="Catalog" type="ST_Catalog" />

  <xs:simpleType name="ST_Catalog">
    <xs:restriction base="xs:string">
      <xs:pattern value="[A-Za-z0-9\+\/\=]+"/>
      <xs:minLength value="4"/>
    </xs:restriction>
  </xs:simpleType>

</xs:schema>
```

次のスキーマは、Windows 10 バージョン1809以降でも有効です。  これにより、SCCD は、承認されたエンティティとなるアプリケーションパッケージを宣言できます。 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified"
  xmlns:xs="http://www.w3.org/2001/XMLSchema"
  targetNamespace="http://schemas.microsoft.com/appx/2018/sccd"
  xmlns:s="http://schemas.microsoft.com/appx/2018/sccd"
  xmlns="http://schemas.microsoft.com/appx/2018/sccd">

  <xs:element name="CustomCapabilityDescriptor" type="CT_CustomCapabilityDescriptor">
    <xs:unique name="Unique_CustomCapability_Name">
      <xs:selector xpath="s:CustomCapabilities/s:CustomCapability"/>
      <xs:field xpath="@Name"/>
    </xs:unique>
  </xs:element>

  <xs:complexType name="CT_CustomCapabilityDescriptor">
    <xs:sequence>
      <xs:element ref="CustomCapabilities" minOccurs="1" maxOccurs="1"/>
      <xs:element ref="AuthorizedEntities" minOccurs="1" maxOccurs="1"/>
      <xs:element ref="DeveloperModeOnly" minOccurs="0" maxOccurs="1"/>
      <xs:element ref="Catalog" minOccurs="1" maxOccurs="1"/>
      <xs:any minOccurs="0"/>
    </xs:sequence>
  </xs:complexType>
  
  <xs:element name="CustomCapabilities" type="CT_CustomCapabilities" />

  <xs:complexType name="CT_CustomCapabilities">
    <xs:sequence>
      <xs:element ref="CustomCapability" minOccurs="1" maxOccurs="unbounded"/>
    </xs:sequence>
  </xs:complexType>

  <xs:element name="CustomCapability">
    <xs:complexType>
      <xs:attribute name="Name" type="ST_CustomCapability" use="required"/>
    </xs:complexType>
  </xs:element>

  <xs:simpleType name="ST_NonEmptyString">
    <xs:restriction base="xs:string">
      <xs:minLength value="1"/>
      <xs:maxLength value="32767"/>
      <xs:pattern value="[^\s]|([^\s].*[^\s])"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:simpleType name="ST_CustomCapability">
    <xs:annotation>
      <xs:documentation>Custom capabilities should be a string in the form of Company.capabilityName_PublisherId</xs:documentation>
    </xs:annotation>
    <xs:restriction base="ST_NonEmptyString">
      <xs:pattern value="[A-Za-z0-9][-_.A-Za-z0-9]*_[a-hjkmnp-z0-9]{13}"/>
      <xs:minLength value="15"/>
      <xs:maxLength value="255"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:element name="AuthorizedEntities" type="CT_AuthorizedEntities" />

  <xs:complexType name="CT_AuthorizedEntities">
    <xs:sequence>
      <xs:element ref="AuthorizedEntity" minOccurs="0" maxOccurs="unbounded"/>
    </xs:sequence>
    <xs:attribute name="AllowAny" type="xs:boolean" use="optional"/>
  </xs:complexType>
  
  <xs:element name="AuthorizedEntity" type="CT_AuthorizedEntity" />
  
  <xs:complexType name="CT_AuthorizedEntity">
    <xs:attribute name="CertificateSignatureHash" type="ST_CertificateSignatureHash" use="required"/>
    <xs:attribute name="AppPackageFamilyName" type="ST_NonEmptyString" use="required"/>
  </xs:complexType>

  <xs:simpleType name="ST_CertificateSignatureHash">
    <xs:restriction base="ST_NonEmptyString">
      <xs:pattern value="[A-Fa-f0-9]+"/>
      <xs:minLength value="64"/>
      <xs:maxLength value="64"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:element name="DeveloperModeOnly">
    <xs:complexType>
      <xs:attribute name="Value" type="xs:boolean" use="required"/>
    </xs:complexType>
  </xs:element>

  <xs:element name="Catalog" type="ST_Catalog" />

  <xs:simpleType name="ST_Catalog">
    <xs:restriction base="xs:string">
      <xs:pattern value="[A-Za-z0-9\+\/\=]+"/>
      <xs:minLength value="4"/>
    </xs:restriction>
  </xs:simpleType>
  
</xs:schema>
```
