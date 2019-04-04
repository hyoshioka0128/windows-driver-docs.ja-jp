---
title: ドライバー開発者向けのハードウェア サポート アプリ (HSA) の手順
description: 対になるドライバーのハードウェア サポート アプリ (HSA) でカスタム機能を作成します。
keywords:
- ユーザー設定 機能
- UWP アプリ
- カスタムの機能
- UWP
- ハードウェア
ms.date: 08/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52811ed7c1c2b481f4b9ef43a588a3079f0aaa3b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548873"
---
# <a name="hardware-support-app-hsa-steps-for-driver-developers"></a>ハードウェア サポートのアプリ (HSA):ドライバー開発者向けの手順

ハードウェア サポート アプリ (HSA) は、特定のドライバーとペアになっているデバイスに固有のアプリまたは[RPC (リモート プロシージャ コール)](https://msdn.microsoft.com/library/windows/desktop/aa378651)エンドポイント。

ドライバーを使用して、ストア アプリを関連付けるには、カスタム機能と呼ばれる特殊な値を最初に予約します。 機能を提供し、機能を提供して、アプリ開発者にアプリへのアクセスを許可します。  このページは、ドライバー開発者向けの次の手順を説明します。

アプリ開発者向けの手順が記載されて[ハードウェア サポート アプリ (HSA)。アプリ開発者のための手順](hardware-support-app--hsa--steps-for-app-developers.md)します。

HSA の 4 つ ("DCHU") の設計原則の 1 つ[ユニバーサル Windows ドライバー](../develop/getting-started-with-universal-drivers.md)します。

## <a name="reserving-a-custom-capability"></a>カスタムの機能を予約します。

最初に、カスタム機能を予約します。

1.  Microsoft ハードウェア サポート アプリ レビューのメール (<HSAReview@microsoft.com>)、次の情報。

    * 連絡先情報
    * 会社名
    * 機能の名前 (する必要がありますで一意であるし、所有者を参照)
    * どのようなリソースにアクセスする機能が必要ですか。
    * セキュリティやプライバシー上の問題
    * データ機能をでへのアクセスを提供しますか。
    * Microsoft Store アプリの発行元 ID が含まれます  いずれかを取得するには、Microsoft Store のページで、アプリのスケルトン エントリを作成します。 アプリの PFN の予約の詳細については、[の名前を予約することで、アプリを作成する](https://msdn.microsoft.com/windows/uwp/publish/create-your-app-by-reserving-a-name)を参照してください。

2.  Microsoft の電子メール要求を承認すると場合、は、バックアップの形式でカスタム機能の一意の文字列名**CompanyName.capabilityName\_PublisherID**します。

現在、RPC エンドポイントまたはドライバーにアクセスできるように、カスタム機能を使用できます。

## <a name="allowing-access-to-an-rpc-endpoint-to-a-uwp-app-using-the-custom-capability"></a>カスタムの機能を使用して UWP アプリへの RPC エンドポイントへのアクセスを許可します。

カスタム機能を持つ UWP アプリへの RPC エンドポイントへのアクセスを許可するのには、次の手順を実行します。

1.  呼び出す[ **DeriveCapabilitySidsFromName** ](https://msdn.microsoft.com/library/windows/desktop/mt803273)セキュリティ ID (SID) にカスタム機能名を変換します。
2.  許可されていると共に、RPC エンドポイントのセキュリティ記述子のために必要なその他の Sid の ACE のアクセスに SID を追加します。
3.  セキュリティ記述子から情報を使用して RPC エンドポイントを作成します。

上記の実装を確認できます、 [RPC サーバー コード](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/CustomCapability/Service/Server/RpcServer.cpp)で、[カスタム機能サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CustomCapability)します。

## <a name="allowing-access-to-a-driver-to-a-uwp-app-using-the-custom-capability"></a>カスタムの機能を使用して UWP アプリへのドライバーへのアクセスを許可します。

カスタム機能を使った UWP アプリへのドライバーへのアクセスを許可するのには、INF ファイルまたはドライバーのソースのいずれかに、いくつかの行を追加します。

INF ファイルで、カスタム機能をよう指定します。

```cpp
[WDMPNPB003_Device.NT.Interfaces] 
AddInterface= {zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz},,AddInterfaceSection 
 
[AddInterfaceSection] 
AddProperty= AddInterfaceSection.AddProps 
 
[AddInterfaceSection.AddProps] 
; DEVPKEY_DeviceInterface_UnrestrictedAppCapabilities 
{026e516e-b814-414b-83cd-856d6fef4822}, 8, 0x2012,, "CompanyName.myCustomCapabilityNameTBD_MyStorePubId"
```

または、ドライバーでは、次の操作を行います。

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

置換`zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz`を公開するインターフェイスの guid。  置換*CompanyName*を自分の会社名、 *myCustomCapabilityNameTBD* 、会社内で一意の名前を持つと*MyStorePubId*パブリッシャーとストア id。 

上述のドライバー コードの例は、、[ユニバーサル ドライバーのドライバー パッケージのインストール ツールキット](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)を参照してください。

## <a name="preparing-the-signed-custom-capability-descriptor-sccd-file"></a>署名済みのカスタム機能記述子 (SCCD) ファイルの準備

署名済みのカスタム機能記述子 (SCCD) ファイルは、符号付きの XML ファイルが 1 つまたは複数のカスタム機能の使用を承認します。  ドライバーまたは RPC エンドポイントの所有者は、このファイルを提供することで、アプリ開発者にカスタム機能を付与します。

SCCD ファイルを準備するには、カスタム機能の文字列をまず更新します。  開始点として、次の例を使用します。

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

次に、カスタム機能の所有者は、パッケージ ファミリ名 (PFN) と署名ハッシュをアプリ開発者から取得し、SCCD ファイルでこれらの文字列を更新します。

**注:** アプリが直接、証明書で署名する必要はありませんが、指定された証明書は、アプリケーションに署名する証明書チェーンの一部である必要があります。

SCCD を完了すると、機能の所有者にメールで送信 Microsoft の署名します。  Microsoft では、機能の所有者に符号付き SCCD を返します。

次に、機能の所有者は、アプリ開発者に、SCCD を送信します。  アプリ開発者には、アプリケーション マニフェストの署名 SCCD が含まれています。  行う必要があるアプリの開発者については、次を参照してください。[ハードウェア サポート アプリ (HSA)。アプリ開発者のための手順](hardware-support-app--hsa--steps-for-app-developers.md)します。

## <a name="limiting-the-scope-of-an-sccd"></a>SCCD のスコープを制限します。

テスト目的で、カスタム機能の所有者は、開発者モードでコンピューターにハードウェアのサポートのアプリのインストールを制限できます。

Microsoft によって署名された SCCD を取得する前に、これには、次のように追加します**DeveloperModeOnly**:。

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

内のデバイスにのみ SCCD works を署名結果[開発者モード](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)します。 

## <a name="allowing-any-app-to-use-a-custom-capability"></a>カスタムの機能を使用するすべてのアプリを許可します。

カスタムの機能を使用して許可されているエンティティ (アプリ) を指定することをお勧めします。 場合によっては、ただし、可能性がある、SCCD を含む任意のアプリを許可します。  Windows 10 バージョンは 1809 以降、これを行う追加して**AllowAny** AuthorizedEntities 要素にします。 使用するための妥当性を指定してください、SCCD ファイルで許可されているエンティティを宣言することをお勧め、ため**AllowAny** SCCD に Microsoft の署名を送信する場合。

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

結果の符号付き SCCD は任意のアプリ パッケージで検証します。 

## <a name="multiple-sccds"></a>複数の SCCDs

アプリは、Windows 10 バージョン 1803 以降、1 つまたは複数の SCCD ファイルからカスタムの機能を宣言できます。 アプリ パッケージのルートに SCCD ファイルを配置します。

## <a name="summary"></a>概要

次の図は、上述の手順をまとめたものです。

![署名済み、SCCD を取得します。](images/signsccd.png)

## <a name="see-also"></a>参照

* [ユニバーサル Windows ドライバーの概要](../develop/getting-started-with-universal-drivers.md)
* [ユニバーサル Windows プラットフォームの紹介](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide)
* [ユニバーサル Windows プラットフォーム (UWP)](https://docs.microsoft.com/windows/uwp/design/basics/design-and-ui-intro)
* [アプリの機能](https://docs.microsoft.com/windows/uwp/packaging/app-capability-declarations)
* [Visual Studio を使用して UWP アプリを開発します。](https://developer.microsoft.com/windows/apps/develop)
* [ユニバーサル Windows プラットフォーム (UWP) アプリとドライバーのペアリング](../install/pairing-app-and-driver-versions.md)
* [UWP アプリを開発します。](https://developer.microsoft.com/windows/apps/develop)
* [Desktop App Converter (デスクトップ ブリッジ) を使用してアプリをパッケージ化](https://docs.microsoft.com/windows/uwp/porting/desktop-to-uwp-run-desktop-app-converter)
* [カスタムの機能のサンプル アプリ](https://go.microsoft.com/fwlink/p/?LinkId=846904)
* [カスタムの機能のドライバーのサンプル](https://aka.ms/customcapabilitydriversample )
* [Windows 10 でアプリをサイドロードします。](https://technet.microsoft.com/library/mt269549.aspx)
* [カスタムの機能に関する FAQ](FAQ-on-custom-capabilities.md)

## <a name="sccd-xml-schema"></a>SCCD XML スキーマ

SCCD ファイルの正式な XML XSD スキーマを次に示します。  このスキーマを使用すると、確認を送信する前に、SCCD を検証します。  参照してください[スキーマ キャッシュ](https://docs.microsoft.com/visualstudio/xml-tools/schema-cache)と[XML ドキュメントの検証](https://docs.microsoft.com/visualstudio/xml-tools/xml-document-validation)スキーマをインポートして、IntelliSense と検証に関する情報について。

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

次のスキーマは、Windows 10、バージョンは 1809 時点で有効でもできます。  承認済みのエンティティである任意のアプリ パッケージを宣言する SCCD できます。 

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
