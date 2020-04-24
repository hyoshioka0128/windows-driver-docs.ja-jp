---
title: PC デバイス マニフェスト パッケージの提出
description: PC デバイス マニフェスト パッケージの提出
ms.assetid: b96b02b8-8804-403e-9513-7a5d1b730fcd
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 147d3c944141cbcc8075f7ab2d47193d599ba2ee
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "75209161"
---
# <a name="submit-a-pc-device-manifest-package"></a>PC デバイス マニフェスト パッケージの提出


## <a name="span-idsubmitting_a_pc_device_manifest_packagespanspan-idsubmitting_a_pc_device_manifest_packagespanspan-idsubmitting_a_pc_device_manifest_packagespansubmitting-a-pc-device-manifest-package"></a><span id="Submitting_a_PC_device_manifest_package"></span><span id="submitting_a_pc_device_manifest_package"></span><span id="SUBMITTING_A_PC_DEVICE_MANIFEST_PACKAGE"></span>PC デバイス マニフェスト パッケージの提出


同じ方法を使って、パッケージをプレビュー用またはリリース用に提出できます。

**デバイス マニフェスト パッケージを申請するには**

1.  [SignTool](https://go.microsoft.com/fwlink/p/?LinkId=238330) ツールを使って、devicemanifest-ms パッケージに署名します。

2.  ハードウェア デベロッパー センターまたは Windows デベロッパー センターから Microsoft アカウントで**ダッシュボード**にサインインします。

3.  **[Device metadata]** (デバイス メタデータ) で、新しいエクスペリエンスを申請する場合は **[Create experience]** (エクスペリエンスの作成)、既にあるエクスペリエンスを変更する場合は **[Manage experience]** (エクスペリエンスの管理) をクリックします。

4.  新しい devicemanifest-ms パッケージを参照して選び、 **[Submit]** (送信) をクリックします。

## <a name="span-idcreating_a_device_manifest_submission_packagespanspan-idcreating_a_device_manifest_submission_packagespanspan-idcreating_a_device_manifest_submission_packagespancreating-a-device-manifest-submission-package"></a><span id="Creating_a_Device_Manifest_Submission_Package"></span><span id="creating_a_device_manifest_submission_package"></span><span id="CREATING_A_DEVICE_MANIFEST_SUBMISSION_PACKAGE"></span>デバイス マニフェスト サブミッション パッケージの作成


デバイス マニフェスト サブミッション パッケージは、すべての PC デバイスのメタデータをハードウェア デベロッパー センターに提出する必要がある場合に使われるパッケージ形式です。

デバイス マニフェスト サブミッション パッケージには、ロケールのサポートを宣言し、提出している会社に PC HWID が属していることを検証できるようにするためのファイルが含まれます。 デバイス マニフェスト パッケージには、デバイス メタデータ パッケージも含まれています。

デバイス マニフェスト サブミッション パッケージは、デバイス メタデータ パッケージと同じ方法でハードウェア デベロッパー センターにアップロードされます。 同じユーザー インターフェイスとアップロード ボックスを使って、アップロードする \*.devicemanifest-ms ファイルの名前を入力します。

ハードウェア デベロッパー センターのユーザー インターフェイスのバルク (一括) アップロード用ボックスを除くすべてのファイル アップロード ボックスで、デバイス マニフェスト サブミッション パッケージを指定できます。

### <a name="span-iddevice_manifest_submission_package_contentsspanspan-iddevice_manifest_submission_package_contentsspanspan-iddevice_manifest_submission_package_contentsspandevice-manifest-submission-package-contents"></a><span id="Device_Manifest_Submission_Package_Contents"></span><span id="device_manifest_submission_package_contents"></span><span id="DEVICE_MANIFEST_SUBMISSION_PACKAGE_CONTENTS"></span>デバイス マニフェスト サブミッション パッケージの内容

デバイス マニフェスト サブミッション パッケージは、それぞれ次のコンポーネントで構成されます。

-   **デバイス メタデータ パッケージ**

    このパッケージには、Windows でのデバイス アイコンの表示、アクションの設定、デバイス エクスペリエンス機能の使用に必要な、情報とグラフィックスが格納されます。

    デバイス メタデータ パッケージは、常に必須です。

-   **LocaleInfo XML ドキュメント**

    このドキュメントには、同梱のデバイス メタデータ パッケージに含まれるロケールのデータが含まれます。 ハードウェア デベロッパー センターでは、このデータに基づいてデバイス メタデータ パッケージのロケールが検証されます。

    デバイス メタデータ パッケージのロケールが 1 つしかない場合でも、LocaleInfo XML ドキュメントは必須です。

-   **PcMetadataSubmission XML ドキュメント**

    このドキュメントには、同梱の PC デバイス メタデータ パッケージ内の HWID を検証するために使われるデータが含まれます。 ハードウェア デベロッパー センターは、このデータを使って、デバイス メタデータ パッケージ内の HWID が正しい会社に属していることを確認します。

    PcMetadataSubmission XML ドキュメントは、PC デバイス メタデータ パッケージにのみ必要です。

**注**   この XML ドキュメントは UTF-8 エンコーディングで保存されている必要があります。

 

### <a name="span-idstructure_of_a_pc_device_manifest_submission_packagespanspan-idstructure_of_a_pc_device_manifest_submission_packagespanspan-idstructure_of_a_pc_device_manifest_submission_packagespanstructure-of-a-pc-device-manifest-submission-package"></a><span id="Structure_of_a_PC_Device_Manifest_Submission_Package"></span><span id="structure_of_a_pc_device_manifest_submission_package"></span><span id="STRUCTURE_OF_A_PC_DEVICE_MANIFEST_SUBMISSION_PACKAGE"></span>PC デバイス マニフェスト サブミッション パッケージの構造

デバイス マニフェスト パッケージの構造は、含まれているデバイス メタデータが PC 用とモバイル ブロードバンド用のどちらであるかと、複数のロケールのサポートが含まれているかどうかに依存します。

デバイス メタデータが 3 つのカテゴリのいずれにも該当しない場合、デバイス マニフェスト パッケージは必要ありません。 ただし、デバイス マニフェスト パッケージは、デバイス メタデータ パッケージが単一のロケール用であることを示すために使うこともできます。

PC デバイス マニフェスト サブミッション パッケージのコンポーネントは、圧縮キャビネット ファイルに格納されています。 ファイル名には .devicemanifest-ms というサフィックスを含める必要があります。

それぞれの PC デバイス マニフェスト サブミッション パッケージに、次の構造が必要です。

``` syntax
GUID1.devicemanifest-ms
  \GUID1.devicemetadata-ms
  \LocaleInfo.xml
  \PcMetadataSubmission.xml
```

"GUID1" には GUID を指定してください。

LocaleInfo.xml と PcMetadataSubmission.xml を作成する方法については、以下をご覧ください。

デバイス メタデータ パッケージ (\*.devicemetadata-ms) を開発する方法について詳しくは、[Windows 8 のデバイス メタデータ パッケージのスキーマ リファレンス](https://go.microsoft.com/fwlink/p/?LinkId=226753)をご覧ください

Cabarc ツールを使って、このような CAB パッケージを作成できます。 このツールについて詳しくは、[Cabarc の概要](https://go.microsoft.com/fwlink/p/?LinkId=248843)に関するページをご覧ください。

Cabarc ツールを使って \*.devicemanifest-ms ファイルを作成した場合、ローカル ディレクトリを作成して、そのルートにデバイス メタデータ パッケージ (\*.devicemetadata-ms)、LocaleInfo XML ドキュメント、PcMetadataSubmission XML ドキュメントを格納する必要があります。

**注釈**

-   .devicemanifest -ms と .devicemetadata-ms のファイル名で指定する GUID は、中かっこ ({}) で区切らないでください。

-   それぞれの PC デバイス マニフェスト サブミッションの GUID とデバイス メタデータ パッケージの GUID は、一意である必要があります。 新しいパッケージまたは変更したパッケージを作成するときには、新しい GUID を作成する必要があります。

-   キャビネット ファイルを作成する方法について詳しくは、[Microsoft キャビネット ソフトウェア開発キット](https://go.microsoft.com/fwlink/p/?LinkId=248844)に関するページをご覧ください。

**例**

Cabarc ツールを使って .devicemanifest-ms ファイルを作成する方法の例を以下に示します。 この例では、PC デバイス マニフェスト ファイルのコンポーネントは、PcPackages という名前のローカル ディレクトリに格納されています。

``` syntax
.\PcPackages\
.\PcPackages\PcMetadataSubmission.xml
.\PcPackages\LocaleInfo.xml
.\PcPackages\GUID.devicemetadata-ms
```

PCFiles という名前のローカル ディレクトリに、GUID.devicemanifest-ms ファイルが作成されています。

``` syntax
Cabarc.exe -r -p -P  .\PcPackages\ 
N .\PCFiles\ GUID.devicemanifest-ms 
.\PcPackages\PcMetadataSubmission.xml
.\PcPackages\LocaleInfo.xml
```

このツールについて詳しくは、[Cabarc の概要](https://go.microsoft.com/fwlink/p/?LinkId=248843)に関するページをご覧ください。

## <a name="span-idcreating_pcmetadatasubmissionxmlspanspan-idcreating_pcmetadatasubmissionxmlspancreating-pcmetadatasubmissionxml"></a><span id="creating_pcmetadatasubmission.xml"></span><span id="CREATING_PCMETADATASUBMISSION.XML"></span>PcMetadataSubmission.xml の作成


### <a name="span-idpcmetadatasubmission_xml_schemaspanspan-idpcmetadatasubmission_xml_schemaspanspan-idpcmetadatasubmission_xml_schemaspanpcmetadatasubmission-xml-schema"></a><span id="PcMetadataSubmission_XML_Schema"></span><span id="pcmetadatasubmission_xml_schema"></span><span id="PCMETADATASUBMISSION_XML_SCHEMA"></span>PcMetadataSubmission XML スキーマ

デバイス マニフェスト サブミッション パッケージには、PcMetadataSubmission.xml ドキュメントを 1 つ含めることができます。このドキュメントの情報は、PackageInfo.xml 内の Computer HardwareID を検証する際にハードウェア デベロッパー センター サイトで使われます。

PcMetadataSubmission.xml ドキュメント内のデータは、以降で説明する PcMetadataSubmission XML スキーマに基づいて書式が設定されます。

**注**   XML ドキュメントは UTF-8 エンコーディングで保存されている必要があります。

 

ComputerHardwareID について詳しくは、[[デバイスとプリンター] 用デバイス メタデータ パッケージの作成方法に関するページ](https://go.microsoft.com/fwlink/p/?LinkId=253559)をご覧ください。

**PcMetadataSubmission XML スキーマの名前空間**

PcMetadataSubmission XML スキーマの名前空間は、以下のとおりです。

-   `http://schemas.microsoft.com/Windows/2009/05/MetadataSubmission/PcMetadataSubmission`

-   `http://schemas.microsoft.com/Windows/2011/06/MetadataSubmission/PcMetadataSubmissionv2`

**PcMetadataSubmission XML の要素/属性の概要**

次の表では、PcMetadataSubmission XML スキーマのメタデータの要素と属性について説明します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>要素/属性</th>
<th>要素/属性の型</th>
<th>必須/省略可能</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SMBIOSEntry</p></td>
<td><p>SMBIOSEntryType</p></td>
<td><p>必須</p></td>
<td><p>コンピューターの SMBIOS 情報を指定します。</p></td>
</tr>
<tr class="even">
<td><p>SystemManufacturer</p></td>
<td><p>tns:SMBIOSStringType</p></td>
<td><p>必須</p></td>
<td><p>コンピューターの名前を指定します。</p></td>
</tr>
<tr class="odd">
<td><p>SystemFamily</p></td>
<td><p>tns:SMBIOSStringType</p></td>
<td><p>オプション</p></td>
<td><p>コンピューターの製造元のファミリ名を指定します。</p></td>
</tr>
<tr class="even">
<td><p>SystemProductName</p></td>
<td><p>tns:SMBIOSStringType</p></td>
<td><p>オプション</p></td>
<td><p>製品 (コンピューター) の名前を指定します。</p></td>
</tr>
<tr class="odd">
<td><p>BIOSVendor</p></td>
<td><p>tns:SMBIOSStringType</p></td>
<td><p>オプション</p></td>
<td><p>BIOS の製造元の名前を指定します。</p></td>
</tr>
<tr class="even">
<td><p>BIOSVersion</p></td>
<td><p>tns:SMBIOSStringType</p></td>
<td><p>オプション</p></td>
<td><p>BIOS のバージョン番号を指定します。</p></td>
</tr>
<tr class="odd">
<td><p>SystemBIOSMajorRelease</p></td>
<td><p>tns:BIOSReleaseType</p></td>
<td><p>オプション</p></td>
<td><p>BIOS の MajorRelease バージョンを指定します。</p></td>
</tr>
<tr class="even">
<td><p>SystemBIOSMinorRelease</p></td>
<td><p>tns:BIOSReleaseType</p></td>
<td><p>オプション</p></td>
<td><p>BIOS の MinorRelease バージョンを指定します。</p></td>
</tr>
<tr class="odd">
<td><p>Enclosuretype</p></td>
<td><p>tns:TypeofEnclosureType</p></td>
<td><p>オプション</p></td>
<td><p>コンピューターの筐体の種類を指定します。</p></td>
</tr>
<tr class="even">
<td><p>SKUNumber</p></td>
<td><p>v2:SMBIOSStringType</p></td>
<td><p>オプション</p></td>
<td><p>コンピューターの SKU 番号を指定します。</p></td>
</tr>
</tbody>
</table>

 

**PcMetadataSubmission XML スキーマの定義**

PcMetadataSubmission XML スキーマの定義は、以下のとおりです。

``` syntax
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema targetNamespace="http://schemas.microsoft.com/Windows/2009/05/MetadataSubmission/PcMetadataSubmission" xmlns:tns="http://schemas.microsoft.com/Windows/2009/05/MetadataSubmission/PcMetadataSubmission" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:v2="http://schemas.microsoft.com/Windows/2011/06/MetadataSubmission/PcMetadataSubmissionv2" elementFormDefault="qualified" blockDefault="#all">

  <xs:element name="PcMetadataSubmission" type="tns:PcMetadataSubmissionType" />
  <xs:complexType name="PcMetadataSubmissionType">
    <xs:sequence>
      <xs:element name="SMBIOSList" type="tns:SMBIOSListType" />
      <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
    </xs:sequence>
  </xs:complexType>

  <xs:complexType name="SMBIOSListType">
    <xs:sequence>
      <xs:element name="SMBIOSEntry" type="tns:SMBIOSEntryType" maxOccurs="unbounded" />
      <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
    </xs:sequence>
  </xs:complexType>

  <xs:complexType name="SMBIOSEntryType">
    <xs:simpleContent>
      <xs:extension base="xs:string">
        <xs:attribute name="SystemManufacturer" type="tns:SMBIOSStringType" use="required" />
        <xs:attribute name="SystemFamily" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="SystemProductName" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="BIOSVendor" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="BIOSVersion" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="SystemBIOSMajorRelease" type="tns:BIOSReleaseType" use="optional" />
        <xs:attribute name="SystemBIOSMinorRelease" type="tns:BIOSReleaseType" use="optional" />
        <xs:attribute name="EnclosureType" type="tns:TypeofEnclosureType" use="optional" />
        <xs:attribute ref="v2:SKUNumber" use="optional" />
      </xs:extension>
    </xs:simpleContent>
  </xs:complexType>
  <xs:simpleType name="SMBIOSStringType">
    <xs:restriction base="xs:string">
      <xs:minLength value="1" />
      <xs:maxLength value="64" />
    </xs:restriction>
  </xs:simpleType>
  <xs:simpleType name="BIOSReleaseType">
    <xs:restriction base="xs:hexBinary">
      <xs:minLength value="1" />
      <xs:maxLength value="1" />
    </xs:restriction>
  </xs:simpleType>
  <xs:simpleType name="TypeofEnclosureType">
    <xs:restriction base="xs:hexBinary">
      <xs:pattern value="([0-7][0-9A-F]|0[0-9A-F])" />
    </xs:restriction>
  </xs:simpleType>
</xs:schema>
```

PcMetadataSubmissionv2 XML スキーマの定義は、以下のとおりです。

``` syntax
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema targetNamespace="http://schemas.microsoft.com/Windows/2011/06/MetadataSubmission/PcMetadataSubmissionv2" xmlns:tns="http://schemas.microsoft.com/Windows/2011/06/MetadataSubmission/PcMetadataSubmissionv2" xmlns:xs="http://www.w3.org/2001/XMLSchema" elementFormDefault="qualified" blockDefault="#all">

  <xs:attribute name="SKUNumber" type="tns:SMBIOSStringType" />

  <xs:simpleType name="SMBIOSStringType">
    <xs:restriction base="xs:string">
      <xs:minLength value="1" />
      <xs:maxLength value="64" />
    </xs:restriction>
  </xs:simpleType>

</xs:schema>
```

### <a name="span-idpcmetadatasubmission_xml_schema_referencespanspan-idpcmetadatasubmission_xml_schema_referencespanspan-idpcmetadatasubmission_xml_schema_referencespanpcmetadatasubmission-xml-schema-reference"></a><span id="PcMetadataSubmission_XML_Schema_Reference"></span><span id="pcmetadatasubmission_xml_schema_reference"></span><span id="PCMETADATASUBMISSION_XML_SCHEMA_REFERENCE"></span>PcMetadataSubmission XML スキーマ リファレンス

PcMetadataSubmission XML スキーマで定義される要素と属性は以下のとおりです。

-   SMBIOSList

    -   SMBIOSEntry

        -   SystemManufacturer

        -   SystemFamily

        -   SystemProductName

        -   BIOSVendor

        -   BIOSVersion

        -   SystemBIOSMajorRelease

        -   SystemBIOSMinorRelease

        -   Enclosuretype

        -   SKUNumber

**SMBIOSEntry の要素**

SMBIOSEntry 要素は、コンピューターのシステム情報を指定します。 この情報に基づいて、ハードウェア デベロッパー センターはコンピューター ハードウェア ID を作成し、その値を、PcMetadataSubmission.xml と共に申請された packageinfo.xml 内のコンピューター ハードウェア ID と比較します。

``` syntax
<xs:element name="SMBIOSEntry" type="tns:SMBIOSEntryType" maxOccurs="unbounded" />

<xs:complexType name="SMBIOSEntryType">
    <xs:simpleContent>
      <xs:extension base="xs:string">
        <xs:attribute name="SystemManufacturer" type="tns:SMBIOSStringType" use="required" />
        <xs:attribute name="SystemFamily" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="SystemProductName" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="BIOSVendor" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="BIOSVersion" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="SystemBIOSMajorRelease" type="tns:BIOSReleaseType" use="optional" />
        <xs:attribute name="SystemBIOSMinorRelease" type="tns:BIOSReleaseType" use="optional" />
        <xs:attribute name="Enclosuretype" type="tns:TypeofEnclosureType" use="optional" />
        <xs:anyAttribute namespace="##other" processContents="lax" />
      </xs:extension>
    </xs:simpleContent>
  </xs:complexType>
```

**注釈**

複数の SMBIOSEntry 要素を使って複数のシステムを指定できます。

たとえば、メタデータ パッケージが複数の PC システムをサポートするとします。 次の SMBIOSEntry 要素を使って、PC システムを定義できます。

``` syntax
<SMBIOSList>
  <SMBIOSEntry
      SystemManufacturer="FABRIKAM" SystemFamily…
  />
  <SMBIOSEntry
      SystemManufacturer="FABRIKAM" SystemFamily…
</SMBIOSList>
```

**SystemManufacturer の属性**

SystemManufacturer の属性は、コンピューターのファミリ名を指定します。

``` syntax
<xs:attribute name="SystemManufacturer" type="tns:SMBIOSStringType" use="required" />

<xs:simpleType name="SMBIOSStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="64" />
  </xs:restriction>
</xs:simpleType>
```

**注釈**

SystemManufacturer 属性によって指定される値は、ターゲット PC の SMBIOS テーブルにある Manufacturer (製造元) フィールドの値と同一である必要があります。 次の表は、Manufacturer (製造元) フィールドの SMBIOS のフィールド情報を示しています。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th>フィールド名</th>
<th>構造体の名前とタイプ</th>
<th>SMBIOS 仕様のバージョン</th>
<th>Offset</th>
<th>長さ</th>
<th>値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>製造元</p></td>
<td><p>システム情報 (タイプ 1)</p></td>
<td><p>2.0+</p></td>
<td><p>04h</p></td>
<td><p>BYTE</p></td>
<td><p>STRING</p></td>
<td><p>dmiStrucBuffer 配列内の、NULL で終了する文字列のインデックス。 この文字列は、コンピューターの製造元の名前を指定します。</p></td>
</tr>
</tbody>
</table>

 

dmiStrucBuffer 配列と SMBIOS フィールドについて詳しくは、[System Management BIOS (SMBIOS) 仕様](https://go.microsoft.com/fwlink/p/?LinkId=145867)をご覧ください。

**SystemFamily の属性**

SystemFamily の属性は、コンピューターの製造元の名前を指定します。

``` syntax
<xs:attribute name="SystemFamily" type="tns:SMBIOSStringType" use="optional" />

<xs:simpleType name="SMBIOSStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="64" />
  </xs:restriction>
</xs:simpleType>
```

**注釈**

SystemFamily 属性によって指定される値は、ターゲット PC の SMBIOS テーブルにある Family (ファミリ) フィールドの値と同一である必要があります。 次の表は、Family (ファミリ) フィールドの SMBIOS のフィールド情報を示しています。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th>フィールド名</th>
<th>構造体の名前とタイプ</th>
<th>SMBIOS 仕様のバージョン</th>
<th>Offset</th>
<th>長さ</th>
<th>値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Family</p></td>
<td><p>システム情報 (タイプ 1)</p></td>
<td><p>2.4+</p></td>
<td><p>1Ah</p></td>
<td><p>BYTE</p></td>
<td><p>STRING</p></td>
<td><p>dmiStrucBuffer 配列内の、NULL で終了する文字列のインデックス。 この文字列は、特定のコンピューターが属しているファミリを指定します。ファミリとは、ハードウェアまたはソフトウェアの観点から、似ていても同一とは言えないコンピューターのセットのことです。通常、ファミリは構成や価格が異なる複数のコンピューター モデルで構成されます。 同じファミリのコンピューターは、多くの場合、ブランドや外観の面で類似した特徴があります。</p></td>
</tr>
</tbody>
</table>

 

dmiStrucBuffer 配列と SMBIOS フィールドについて詳しくは、[System Management BIOS (SMBIOS) 仕様](https://go.microsoft.com/fwlink/p/?LinkId=145867)をご覧ください。

**SystemProductName の属性**

SystemProductName の属性は、製品 (コンピューター) の名前を指定します。

``` syntax
<xs:attribute name="SystemProductName" type="tns:SMBIOSStringType" use="optional" />

<xs:simpleType name="SMBIOSStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="64" />
  </xs:restriction>
</xs:simpleType>
```

**注釈**

SystemProductName 属性によって指定される値は、ターゲット PC の SMBIOS テーブルにある Product Name (製品名) フィールドの値と同一である必要があります。 次の表は、Product Name (製品名) フィールドの SMBIOS のフィールド情報を示しています。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th>フィールド名</th>
<th>構造体の名前とタイプ</th>
<th>SMBIOS 仕様のバージョン</th>
<th>Offset</th>
<th>長さ</th>
<th>値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>製品名</p></td>
<td><p>システム情報 (タイプ 1)</p></td>
<td><p>2.0+</p></td>
<td><p>05h</p></td>
<td><p>BYTE</p></td>
<td><p>STRING</p></td>
<td><p>dmiStrucBuffer 配列内の、NULL で終了する文字列のインデックス。 この文字列は、コンピューターの製品名を指定します。</p></td>
</tr>
</tbody>
</table>

 

dmiStrucBuffer 配列と SMBIOS フィールドについて詳しくは、[System Management BIOS (SMBIOS) 仕様](https://go.microsoft.com/fwlink/p/?LinkId=145867)をご覧ください。

**BIOSVendor の属性**

BIOSVendor の属性は、BIOS の製造元の名前を指定します。

``` syntax
<xs:attribute name="BIOSVendor" type="tns:SMBIOSStringType" use="optional" />

<xs:simpleType name="SMBIOSStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="64" />
  </xs:restriction>
</xs:simpleType>
```

**注釈**

BIOSVendor 属性によって指定される値は、ターゲット PC の SMBIOS テーブルにある Vendor (ベンダー) フィールドの値と同一である必要があります。 次の表は、Vendor (ベンダー) フィールドの SMBIOS のフィールド情報を示しています。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th>フィールド名</th>
<th>構造体の名前とタイプ</th>
<th>SMBIOS 仕様のバージョン</th>
<th>Offset</th>
<th>長さ</th>
<th>値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ベンダー</p></td>
<td><p>BIOS 情報 (タイプ 0)</p></td>
<td><p>2.0</p></td>
<td><p>04h</p></td>
<td><p>BYTE</p></td>
<td><p>STRING</p></td>
<td><p>dmiStrucBuffer 配列内の、NULL で終了する文字列のインデックス。 この文字列は、BIOS のベンダーの名前を指定します。</p></td>
</tr>
</tbody>
</table>

 

dmiStrucBuffer 配列と SMBIOS フィールドについて詳しくは、[System Management BIOS (SMBIOS) 仕様](https://go.microsoft.com/fwlink/p/?LinkId=145867)をご覧ください。

**BIOSVersion の属性**

BIOSVersion の属性は、BIOS のバージョン番号を指定します。

``` syntax
<xs:attribute name="BIOSVersion" type="tns:SMBIOSStringType" use="optional" />

<xs:simpleType name="SMBIOSStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="64" />
  </xs:restriction>
</xs:simpleType>
```

**注釈**

BIOSVersion 属性によって指定される値は、ターゲット PC の SMBIOS テーブルにある BIOS Version (BIOS のバージョン) フィールドの値と同一である必要があります。 次の表は、BIOS Version (BIOS のバージョン) フィールドの SMBIOS のフィールド情報を示しています。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th>フィールド名</th>
<th>構造体の名前とタイプ</th>
<th>SMBIOS 仕様のバージョン</th>
<th>Offset</th>
<th>長さ</th>
<th>値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>BIOS Version (BIOS のバージョン)</p></td>
<td><p>BIOS 情報 (タイプ 0)</p></td>
<td><p>2.0</p></td>
<td><p>05h</p></td>
<td><p>BYTE</p></td>
<td><p>STRING</p></td>
<td><p>dmiStrucBuffer 配列内の、NULL で終了する文字列のインデックス。 この文字列には、プロセッサ コアと OEM バージョンについての情報を含めることができます。</p></td>
</tr>
</tbody>
</table>

 

dmiStrucBuffer 配列と SMBIOS フィールドについて詳しくは、[System Management BIOS (SMBIOS) 仕様](https://go.microsoft.com/fwlink/p/?LinkId=145867)をご覧ください。

**SystemBIOSMajorRelease の属性**

SystemBIOSMajorRelease の属性は、BIOS のメジャー リリース バージョンを指定します。

``` syntax
<xs:attribute name="SystemBIOSMajorRelease" type="tns:BIOSReleaseType" use="optional" />

<xs:simpleType name="BIOSReleaseType">
  <xs:restriction base="xs:hexBinary">
    <xs:minLength value="1" />
    <xs:maxLength value="1" />
  </xs:restriction>
</xs:simpleType>
```

**注釈**

SystemBIOSMajorRelease 属性によって指定される値は、ターゲット PC の SMBIOS テーブルにある SystemBIOSMajorRelease (システム BIOS のメジャー リリース) フィールドの値と同一である必要があります。 次の表は、SystemBIOSMajorRelease (システム BIOS のメジャー リリース) フィールドの SMBIOS のフィールド情報を示しています。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th>フィールド名</th>
<th>構造体の名前とタイプ</th>
<th>SMBIOS 仕様のバージョン</th>
<th>Offset</th>
<th>長さ</th>
<th>値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>System BIOS Major Release (システム BIOS のメジャー リリース)</p></td>
<td><p>BIOS 情報 (タイプ 0)</p></td>
<td><p>2.4</p></td>
<td><p>14h</p></td>
<td><p>BYTE</p></td>
<td><p>状況により異なる。</p></td>
<td><p>システム BIOS のメジャー リリース。</p></td>
</tr>
</tbody>
</table>

 

SMBIOS フィールドについて詳しくは、[System Management BIOS (SMBIOS) 仕様](https://go.microsoft.com/fwlink/p/?LinkId=145867)をご覧ください。

**SystemBIOSMinorRelease の属性**

SYSTEMBIOSMinorRelease の属性は、BIOS のマイナー リリース バージョンを指定します。

``` syntax
<xs:attribute name="SystemBIOSMinorRelease" type="tns:BIOSReleaseType" use="optional" />

<xs:simpleType name="BIOSReleaseType">
  <xs:restriction base="xs:hexBinary">
    <xs:minLength value="1" />
    <xs:maxLength value="1" />
  </xs:restriction>
</xs:simpleType>
```

**注釈**

SystemBIOSMinorRelease 属性によって指定される値は、ターゲット PC の SMBIOS テーブルにある SystemBIOSMinorRelease (システム BIOS のマイナー リリース) フィールドの値と同一である必要があります。 次の表は、SystemBIOSMinorRelease (システム BIOS のマイナー リリース) フィールドの SMBIOS のフィールド情報を示しています。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th>フィールド名</th>
<th>構造体の名前とタイプ</th>
<th>SMBIOS 仕様のバージョン</th>
<th>Offset</th>
<th>長さ</th>
<th>値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>System BIOS Minor Release (システム BIOS のマイナー リリース)</p></td>
<td><p>BIOS 情報 (タイプ 0)</p></td>
<td><p>2.4</p></td>
<td><p>15h</p></td>
<td><p>BYTE</p></td>
<td><p>状況により異なる。</p></td>
<td><p>システム BIOS のマイナー リリース。</p></td>
</tr>
</tbody>
</table>

 

SMBIOS フィールドについて詳しくは、[System Management BIOS (SMBIOS) 仕様](https://go.microsoft.com/fwlink/p/?LinkId=145867)をご覧ください。

**Enclosuretype の属性**

Enclosuretype の属性は、コンピューターの筐体の種類を指定します。

``` syntax
<xs:attribute name="EnclosureType" type="tns:TypeofEnclosureType" use="optional" />

<xs:simpleType name="TypeofEnclosureType">
  <xs:restriction base="xs:hexBinary">
    <xs:pattern value="([0-7][0-9A-F]|0[0-9A-F])" />
  </xs:restriction>
</xs:simpleType>
```

**注釈**

Enclosuretype 属性によって指定される値は、ターゲット PC の SMBIOS テーブルにある Enclosure (筐体) フィールドの値と同一である必要があります。 次の表は、Enclosure (筐体) フィールドの SMBIOS のフィールド情報を示しています。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th>フィールド名</th>
<th>構造体の名前とタイプ</th>
<th>SMBIOS 仕様のバージョン</th>
<th>Offset</th>
<th>長さ</th>
<th>値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Enclosure type (筐体の種類)</p></td>
<td><p>システム筐体 (タイプ 3)</p></td>
<td><p>2.0+</p></td>
<td><p>05h</p></td>
<td><p>BYTE</p></td>
<td><p>状況により異なる。</p></td>
<td><p>システムの筐体またはシャーシの種類。</p></td>
</tr>
</tbody>
</table>

 

SMBIOS フィールドについて詳しくは、[System Management BIOS (SMBIOS) 仕様](https://go.microsoft.com/fwlink/p/?LinkId=145867)をご覧ください。

**SKUNumber 要素**

SKUNumber 要素は、コンピューターの SKU 番号を指定します。

``` syntax
<xs:attribute name="SKUNumber" type="tns:SMBIOSStringType" />

<xs:simpleType name="SMBIOSStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="64" />
  </xs:restriction>
</xs:simpleType>
```

**注釈**

SKUNumber 要素によって指定される値は、ターゲット PC の SMBIOS テーブルにある SKU Number (SKU 番号) フィールドの値と同一である必要があります。 次の表は、SKU Number (SKU 番号) フィールドの SMBIOS のフィールド情報を示しています。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th>フィールド名</th>
<th>構造体の名前とタイプ</th>
<th>SMBIOS 仕様のバージョン</th>
<th>Offset</th>
<th>長さ</th>
<th>値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SKU Number (SKU 番号)</p></td>
<td><p>システム情報 (タイプ 1)</p></td>
<td><p>2.4+</p></td>
<td><p>19h</p></td>
<td><p>BYTE</p></td>
<td><p>STRING</p></td>
<td><p>NULL で終了する文字列の番号。このテキスト文字列は、販売のための特定のコンピューター構成を識別するために使われます。 製品 ID または発注番号と呼ばれる場合もあります。 この番号は、既存のフィールドでしばしば使われますが、標準の形式はありません。 一般に、どの OEM のシステム ボードでも、プロセッサ、メモリ、ハード ドライブ、光学式ドライブの組み合わせは無数にあります。</p></td>
</tr>
</tbody>
</table>

 

SMBIOS フィールドについて詳しくは、[System Management BIOS (SMBIOS) 仕様](https://go.microsoft.com/fwlink/p/?LinkId=145867)をご覧ください。

### <a name="span-idpcmetadatasubmission_xml_examplespanspan-idpcmetadatasubmission_xml_examplespanspan-idpcmetadatasubmission_xml_examplespanpcmetadatasubmission-xml-example"></a><span id="PcMetadataSubmission_XML_Example"></span><span id="pcmetadatasubmission_xml_example"></span><span id="PCMETADATASUBMISSION_XML_EXAMPLE"></span>PcMetadataSubmission XML の例

次に示す XML ドキュメントでは、PcMetadataSubmission XML スキーマを使って、ターゲット コンピューターの PcMetadataSubmission 情報のコンポーネントを指定しています。

``` syntax
<?xml version="1.0" encoding="utf-8"?>
<PcMetadataSubmission xmlns="http://schemas.microsoft.com/Windows/2009/05/MetadataSubmission/PcMetadataSubmission">
  <SMBIOSList>
   <SMBIOSEntry
      SystemManufacturer="FABRIKAM"
      SystemFamily="FABRIKAM A SERIES"
      SystemProductName="FABRIKAM LAPTOP"
      BIOSVendor="FABRIKAM"
      BIOSVersion="7BETC7WW (2.08 )"
      SystemBIOSMajorRelease="08"
      SystemBIOSMinorRelease="00"
      EnclosureType="0A"
      v2:SKUNumber="1234567890ABCD"
    />
  </SMBIOSList>
</PcMetadataSubmission>
```

## <a name="span-idcreating_localeinfoxmlspanspan-idcreating_localeinfoxmlspancreating-localeinfoxml"></a><span id="creating_localeinfo.xml"></span><span id="CREATING_LOCALEINFO.XML"></span>LocaleInfo.xml の作成


Localeinfo.xml ファイルを申請用に作成する方法について詳しくは、「[LocaleInfo.xml サブミッション ファイルの作成](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)」をご覧ください。

 

 





