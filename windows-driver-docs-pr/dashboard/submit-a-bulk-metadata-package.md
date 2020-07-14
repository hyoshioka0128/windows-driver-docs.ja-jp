---
title: バルク メタデータ パッケージの提出
description: ドライバー用のバルク メタデータ パッケージのコンポーネントを作成します。これには、デバイス メタデータ パッケージ、デバイス マニフェスト パッケージ、BulkMetadataSubmission XML ドキュメントがあります。
ms.assetid: c8e248d4-a419-48e1-839d-1bbb9adda382
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 035264bb41142706adadb62f72548705eee73e7f
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141303"
---
# <a name="submit-a-bulk-metadata-package"></a>バルク メタデータ パッケージの提出

バルク メタデータ パッケージを提出するには、以下の手順に従ってください。

1. [SignTool](https://go.microsoft.com/fwlink/p/?LinkId=238330) ツールを使って、一括メタデータ パッケージに署名します。

2. ハードウェア デベロッパー センターまたは Windows デベロッパー センターから Microsoft アカウントで**ダッシュボード**にサインインします。

3. **[Device metadata]** (デバイス メタデータ) で **[Create bulk submission]** (一括申請の作成) をクリックします。

4. 新しいバルク メタデータ パッケージを参照して選び、 **[Submit]** (送信) をクリックします。

## <a name="creating-a-bulk-submission-package"></a>バルク メタデータ サブミッション パッケージの作成

バルク メタデータ サブミッション パッケージは、複数のデバイス メタデータ パッケージをダッシュボードに提出する場合に使われるパッケージ形式です。

バルク メタデータ サブミッション パッケージは、一括申請機能を使ってダッシュボードにアップロードする必要があります。 この機能では、複数のメタデータ パッケージを同時に簡単にアップロードできるように、エクスペリエンスを作成するためのユーザー インターフェイスが排除されています。 エクスペリエンスを作成しパッケージ属性を変更するために使われる情報は、BulkMetadataSubmission XML ドキュメントに格納されます。

最大で 50 個の devicemetadata-ms ファイルまたは devicemanifest-ms ファイルをバルク パッケージに含めることができます。

Device Metadata Submission (デバイス メタデータの提出) ウィザードを使って一括メタデータ パッケージを作る方法について詳しくは、[Visual Studio でのデバイス メタデータ提出パッケージの作成に関するページ](https://go.microsoft.com/fwlink/p/?LinkId=251705)をご覧ください。

### <a name="bulk-metadata-submission-package-contents"></a>バルク メタデータ サブミッション パッケージの内容

バルク メタデータ サブミッション パッケージは、それぞれ次のコンポーネントで構成されます。

- デバイス メタデータ パッケージ

    デバイス メタデータ パッケージには、デバイス アイコンの表示、アクションの設定、デバイス エクスペリエンス機能の使用に必要な情報とグラフィックスが格納されます。

- デバイス マニフェスト パッケージ

    デバイス マニフェスト パッケージには、デバイス メタデータ パッケージの検証に使われる情報が格納されます。

- BulkMetadataSubmission XML ドキュメント

    このドキュメントには、ユーザー インターフェイスを使わずにパッケージを適切に提出するためのデータが格納されます。 ダッシュボードでは、このドキュメントに含まれる情報を使って、フレンドリ名を持つエクスペリエンスの作成、パッケージのエクスペリエンスへの構成、エクスペリエンスの更新、個々のパッケージのプレビューとしてのマーキングを行います。

>[!NOTE]
>この XML ドキュメントは UTF-8 エンコーディングで保存されている必要があります。

バルク メタデータ サブミッション パッケージには、1 つ以上のデバイス メタデータ パッケージまたはデバイス マニフェスト パッケージを含める必要があります。

### <a name="structure-of-a-bulk-metadata-submission-package"></a>バルク メタデータ サブミッション パッケージの構造

バルク メタデータ サブミッション パッケージのコンポーネントは、圧縮キャビネット ファイルに格納されています。 ファイル名には ".bulkmetadata-ms" というサフィックスを含める必要があります。

それぞれのバルク メタデータ サブミッション パッケージに、次の構造が必要です。

```syntax
DDMMYYYY.bulkmetadata-ms
\Filename1.devicemetadata-ms
\Filename2.devicemetadata-ms
\...
\Filename3.devicemanifest-ms
\Filename4.devicemanifest-ms
\...
\BulkMetadataSubmission.xml
```

Filename1、Filename2、Filename3、Filename4... は、GUID である必要があります。

BulkMetadataSubmission.xml を作成するには、以下の「[BulkMetadataSubmission.xml の作成](#creating-bulkmetadatasubmissionxml)」を参照してください。

デバイス メタデータ パッケージ (\*.devicemetadata-ms) を開発する方法について詳しくは、[Windows 8 のデバイス メタデータ パッケージのスキーマ レファレンス](https://go.microsoft.com/fwlink/p/?LinkId=226753)に関するページをご覧ください。

デバイス マニフェスト パッケージ (\*.devicemanifest-ms) を開発するには、「[PC デバイス マニフェスト パッケージの提出](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)」をご覧ください。

Cabarc ツールを使って、このような CAB パッケージを作成できます。 このツールについて詳しくは、[Cabarc の概要](https://go.microsoft.com/fwlink/p/?LinkId=248843)に関するページをご覧ください。

Cabarc ツールを使って \*.bulkmetadata-ms ファイルを作成した場合、ローカル ディレクトリを作成して、そのルートにデバイス メタデータ パッケージ (\*.devicemetadata-ms)、デバイス マニフェスト パッケージ (\*.devicemanifest-ms)、BulkMetadataSubmission XML ドキュメントを格納する必要があります。

## <a name="remarks"></a>コメント

- .devicemetadata-ms と .devicemanifest-ms のファイル名で指定する GUID は、中かっこ ({}) で区切らないでください。

- それぞれのデバイス メタデータ パッケージの GUID とデバイス マニフェスト パッケージの GUID は、一意である必要があります。 新しいパッケージまたは変更したパッケージを作成するときには、新しい GUID を作成する必要があります。

- キャビネット ファイルを作成する方法について詳しくは、[Microsoft キャビネット SDK](https://go.microsoft.com/fwlink/p/?LinkId=248844)に関するページをご覧ください。

## <a name="example"></a>例

Cabarc ツールを使って .bulkmetadata-ms ファイルを作成する方法の例を以下に示します。 この例では、バルク メタデータ ファイルのコンポーネントは、BulkPackages という名前のローカル ディレクトリに格納されています。

```syntax
.\BulkPackages\
.\BulkPackages\BulkMetadataSubmission.xml
.\BulkPackages\GUID1.devicemetadata-ms
.\BulkPackages\GUID2.devicemetadata-ms
.\BulkPackages\GUID3.devicemanifest-ms
.\BulkPackages\GUID4.devicemanifest-ms
```

PCFiles という名前のローカル ディレクトリに、GUID.pcmetadata-ms ファイルが作成されています。

```syntax
Cabarc.exe -r -p -P  .\BulkPackages\
N .\BulkFiles\ DDMMYYYY.bulkmetadata-ms
.\BulkPackages\BulkMetadataSubmission.xml
.\BulkPackages\GUID1.devicemetadata-ms
.\BulkPackages\GUID2.devicemetadata-ms
.\BulkPackages\GUID3.devicemanifest-ms
.\BulkPackages\GUID4.devicemanifest-ms
```

>[!Note]
>このツールについて詳しくは、[Cabarc の概要](https://go.microsoft.com/fwlink/p/?LinkId=248843)に関するページをご覧ください。

## <a name="creating-bulkmetadatasubmissionxml"></a>BulkMetadataSubmission.xml の作成

### <a name="bulkmetadatasubmission-xml-schema"></a>BulkMetadataSubmission XML スキーマ

バルク メタデータ サブミッション パッケージには、BulkMetadataSubmission.xml という名前のドキュメントが 1 つ含まれています。ダッシュボードは、このドキュメントに含まれている情報に基づいて、フレンドリ名を持つエクスペリエンスの作成、パッケージのエクスペリエンスへの構成、エクスペリエンスの更新、個々のパッケージのプレビューとしてのマーキングを行います。

BulkMetadataSubmission.xml ドキュメント内のデータは、以降で説明する BulkMetadataSubmission XML スキーマに基づいて書式が設定されます。

>[!NOTE]
>XML ドキュメントは UTF-8 エンコーディングで保存されている必要があります。

### <a name="bulkmetadatasubmission-xml-schema-namespace"></a>BulkMetadataSubmission XML スキーマの名前空間

PcMetadataSubmission XML スキーマの名前空間は、次のようになります: `http://schemas.microsoft.com/Windows/2010/08/MetadataSubmission/BulkMetadataSubmission`

### <a name="overview-of-bulkmetadatasubmission-xml-elementsattributes"></a>BulkMetadataSubmission XML の要素/属性の概要

次の表では、BulkMetadataSubmission XML スキーマのメタデータの要素と属性について説明します。

|要素/属性|要素/属性の型|必須/省略可能|
|----|----|----|
|エクスペリエンス|ExperienceType|必須|
|ExperienceName|xs:string|必須|
|ExperienceId|tns:GUIDType|オプション|
|PackageList|tns:PackageListType|必須|
|PackageFileName|PackageFileNameType|必須|
|preview|xs:Boolean|必須|
|locale|xs:string|必須|
|Qualification|tns:QualificationType|必須|
|LogoSubmissionIDList|tns:LogoSubmissionIDListType|オプション|
|LogoSubmissionID|xs:integer|必須|
|update|xs:Boolean|必須|

### <a name="bulkmetadatasubmission-xml-schema-metadata"></a>BulkMetadataSubmission XML スキーマのメタデータ

BulkMetadataSubmission XML スキーマのメタデータは以下のとおりです。

```syntax
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema targetNamespace="http://schemas.microsoft.com/Windows/2010/08/MetadataSubmission/BulkMetadataSubmission" xmlns:tns="http://schemas.microsoft.com/Windows/2010/08/MetadataSubmission/BulkMetadataSubmission" xmlns:xs="http://www.w3.org/2001/XMLSchema" elementFormDefault="qualified" blockDefault="#all">

 <xs:element name="BulkMetadataSubmission" type="tns:BulkMetadataSubmissionType" />

 <xs:complexType name="BulkMetadataSubmissionType">
  <xs:sequence>
   <xs:element name="Experience" type="tns:ExperienceType"  maxOccurs="unbounded" />
   <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
 </xs:complexType>

  <xs:complexType name="ExperienceType">
    <xs:complexContent>
      <xs:extension base ="tns:BaseExperienceType">
        <xs:attribute name="update" type="xs:boolean" use="required"/>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>

  <xs:complexType name="BaseExperienceType">  
    <xs:sequence>
      <xs:element name="ExperienceName" type="xs:string" />
      <xs:element name="ExperienceId" type="tns:GUIDType" minOccurs="0" />
      <xs:element name="PackageList" type="tns:PackageListType" />
      <xs:element name="Qualification" type="tns:QualificationType" />
      <xs:element name="LogoSubmissionIDList" type="tns:LogoSubmissionIDListType" minOccurs="0" maxOccurs="unbounded" />
      <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
    </xs:sequence>
  </xs:complexType>

  <xs:simpleType name="GUIDType">
    <xs:restriction base="xs:string">
      <xs:pattern value="[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12}" />
    </xs:restriction>
  </xs:simpleType>

 <xs:complexType name="PackageListType">
  <xs:sequence>
   <xs:element name="PackageFileName" type="tns:PackageFileNameType"  maxOccurs="unbounded" />
   <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
 </xs:complexType>

  <xs:complexType name="PackageFileNameType">
    <xs:simpleContent>
      <xs:extension base="xs:string">
        <xs:attribute name="preview" type="xs:boolean" use="required" />
        <xs:attribute name="locale" type="xs:string" use="required" />
      </xs:extension>
    </xs:simpleContent>
  </xs:complexType>

 <xs:simpleType name="QualificationType">
<xs:union memberTypes="tns:QualificationTypeEnumeration xs:string" />
 </xs:simpleType>

 <xs:simpleType name="QualificationTypeEnumeration">
   <xs:restriction base="xs:string">
     <xs:enumeration value="Logo/IDDA" />
     <xs:enumeration value="MicrosoftInboxDriver" />
   </xs:restriction>
 </xs:simpleType>

 <xs:complexType name="LogoSubmissionIDListType">
  <xs:sequence>
   <xs:element name="LogoSubmissionID" type="xs:integer"  maxOccurs="unbounded" />
   <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
 </xs:complexType>

</xs:schema>
```

### <a name="bulkmetadatasubmission-xml-schema-reference"></a>BulkMetadataSubmission XML スキーマ リファレンス

BulkMetadataSubmission XML スキーマで定義される要素と属性は以下のとおりです。

- BulkMetadataSubmission

  - エクスペリエンス

    - ExperienceName

    - ExperienceID

    - PackageList

      - PackageFileName

        - preview

        - locale

    - Qualification

    - LogoSubmissionIDList

      - LogoSubmissionID

    - update

### <a name="experience-element"></a>Experience 要素

Experience 要素では、単一のエクスペリエンスの情報を指定します。 エクスペリエンスについて詳しくは、[Windows 8 のデバイス メタデータ パッケージのスキーマ レファレンスに関するページ](https://go.microsoft.com/fwlink/p/?LinkId=226753)をご覧ください。

ダッシュボードは、この情報に基づいて、適切な情報でエクスペリエンスを作成し、パッケージをこのエクスペリエンスに提出するか、または既にあるエクスペリエンスを新しいパッケージで更新します。

```syntax
<xs:element name="Experience" type="tns:ExperienceType"  maxOccurs="unbounded" />

<xs:complexType name="ExperienceType">
  <xs:complexContent>
    <xs:extension base ="tns:BaseExperienceType">
      <xs:attribute name="update" type="xs:boolean" use="required"/>
    </xs:extension>
  </xs:complexContent>
</xs:complexType>

<xs:complexType name="BaseExperienceType">  
  <xs:sequence>
    <xs:element name="ExperienceName" type="xs:string" />
    <xs:element name="ExperienceId" type="tns:GUIDType" minOccurs="0" />
    <xs:element name="PackageList" type="tns:PackageListType" />
    <xs:element name="Qualification" type="tns:QualificationType" />
    <xs:element name="LogoSubmissionIDList" type="tns:LogoSubmissionIDListType" minOccurs="0" maxOccurs="unbounded" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

複数の Experience 要素を使って複数のエクスペリエンスを指定できます。 これにより、異なるデバイスに対応する複数のパッケージを 1 回の申請に含めることができます。

たとえば、次のように入力します。

``` syntax
<Experience update="false">
  <ExperienceName>Test1</ExperienceName>
  <PackageList>
    <PackageFileName locale="en-us" preview ="false">
      XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.devicemanifest-ms
    </PackageFileName>
  </PackageList>
  <Qualification>Logo/IDDA</Qualification>
  <LogoSubmissionIDList>
    <LogoSubmissionID>XXXXXXX</LogoSubmissionID>
  </LogoSubmissionIDList>
</Experience>

<Experience update="false">
  <ExperienceName>Test2</ExperienceName>
  <PackageList>
    <PackageFileName locale="en-us" preview ="false">
      XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.devicemetadata-ms
    </PackageFileName>
  </PackageList>
  <Qualification>Logo/IDDA</Qualification>
  <LogoSubmissionIDList>
    <LogoSubmissionID>XXXXXXX</LogoSubmissionID>
  </LogoSubmissionIDList>
</Experience>
```

### <a name="experiencename-element"></a>ExperienceName 要素

ExperienceName 要素では、エクスペリエンスの名前を指定します。 ダッシュボードは、これが新しいエクスペリエンスであればこの名前のエクスペリエンスを作成します。 また、これが既にあるエクスペリエンスの更新であれば、この値を無視します。

``` syntax
<xs:element name="ExperienceName" type="xs:string" />
```

### <a name="experienceid-element"></a>ExperienceId 要素

ExperienceId 要素は、エクスペリエンス ID である GUID を指定します。 この値は、既にあるエクスペリエンスを更新するときに必要になります。 ダッシュボードは、この値を使って、更新するエクスペリエンスを識別します。

``` syntax
<xs:element name="ExperienceId" type="tns:GUIDType" minOccurs="0" />

<xs:simpleType name="GUIDType">
  <xs:restriction base="xs:string">
    <xs:pattern value="[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12}" />
  </xs:restriction>
</xs:simpleType>
```

### <a name="packagelist-element"></a>PackageList 要素

PackageList 要素では、エクスペリエンスに含めるデバイス メタデータ パッケージまたはデバイス マニフェスト パッケージのリストを指定します。 ダッシュボードは、この情報を使って、パッケージを新しいエクスペリエンスや既にあるエクスペリエンスに追加します。

``` syntax
<xs:element name="PackageList" type="tns:PackageListType" />

<xs:complexType name="PackageListType">
  <xs:sequence>
    <xs:element name="PackageFileName" type="tns:PackageFileNameType"  maxOccurs="unbounded" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

### <a name="packagefilename-element"></a>PackageFileName 要素

PackageFileName 要素では、単一のデバイス メタデータ パッケージまたはデバイス マニフェスト パッケージのファイル名と情報を指定します。 ダッシュボードは、この情報を使って、パッケージを新しいエクスペリエンスや既にあるエクスペリエンスに追加し、指定された場合はパッケージをプレビューとして適切にマーキングします。 さらに、ダッシュボードは、preview 値と locale 値に基づいて、必要に応じて既にあるパッケージを削除します。

``` syntax
<xs:element name="PackageFileName" type="tns:PackageFileNameType"  maxOccurs="unbounded" />

<xs:complexType name="PackageFileNameType">
  <xs:simpleContent>
    <xs:extension base="xs:string">
      <xs:attribute name="preview" type="xs:boolean" use="required" />
      <xs:attribute name="locale" type="xs:string" use="required" />
    </xs:extension>
  </xs:simpleContent>
</xs:complexType>
```

ダッシュボードは、PackageFileName 要素の preview 属性と locale 属性に基づいて、既にあるライブ パッケージを新しく提出されたパッケージで更新します。

たとえば、en-US プレビュー パッケージがエクスペリエンスに既に存在し、同じエクスペリエンスに対して en-US プレビュー パッケージがバルク メタデータ サブミッション パッケージで申請された場合、既にあるパッケージは自動的に削除され、新しいパッケージが申請されます。

このため、パッケージが誤って削除されることを防ぐためにも、パッケージを更新する際は注意が必要です。

### <a name="preview-attribute"></a>preview 属性

preview 属性では、デバイス メタデータ パッケージまたはデバイス マニフェスト パッケージをプレビューとしてマーキングするかどうかを指定します。 この値がダッシュボードでどのように使われるかについて詳しくは、「PackageFileName 要素」をご覧ください。

``` syntax
<xs:attribute name="preview" type="xs:boolean" use="required" />
```

### <a name="locale-attribute"></a>locale 属性

locale 属性では、デバイス メタデータ パッケージまたはデバイス マニフェスト パッケージの (PackageInfo.xml で) 宣言されたロケールをプレビューとしてマーキングすることを指定します。 この値がダッシュボードでどのように使われるかについて詳しくは、「PackageFileName 要素」をご覧ください。

``` syntax
<xs:attribute name="locale" type="xs:string" use="required" />
```

### <a name="qualification-element"></a>Qualification 要素

Qualification 要素では、デバイスがロゴ認定を取得しているかどうか、デバイスが Inbox Driver Distribution Agreement (IDDA) リストに含まれているかどうか、デバイスが Microsoft インボックス ドライバーを使うかどうかを指定します。 ダッシュボードは、この情報を使って、申請されたデバイス メタデータの種類に適したデバイス認定を実行します。

``` syntax
<xs:element name="Qualification" type="tns:QualificationType" />

<xs:simpleType name="QualificationType">
<xs:union memberTypes="tns:QualificationTypeEnumeration xs:string" />
 </xs:simpleType>

 <xs:simpleType name="QualificationTypeEnumeration">
   <xs:restriction base="xs:string">
     <xs:enumeration value="Logo/IDDA" />
     <xs:enumeration value="MicrosoftInboxDriver" />
   </xs:restriction>
 </xs:simpleType>
```

ロゴ認定を取得しておらず、IDDA リストに含まれていないデバイスでは、Device Stage などの機能を利用できません。

それぞれのエクスペリエンスに対して 2 つのオプションのどちらかを選ぶことができます。 これらのオプションとその定義を次の表に示します。

|列挙値|説明|
|----|----|
|Logo/IDDA|デバイスはロゴ認定を取得しているか、または IDDA リストに含まれています。 ロゴ認定を取得している場合は、LogoSubmissionIDList 要素に特定のロゴのサブミッション ID を指定する必要があります。|
|MicrosoftInboxDrive|デバイスは Microsoft インボックス ドライバーを使います。 この認定レベルでは、デバイス メタデータの一部の機能を利用できません (たとえば、Device Stage)。|

### <a name="logosubmissionidlist-element"></a>LogoSubmissionIDList 要素

LogoSubmissionIDList 要素は、デバイスのロゴ認定のリストを指定します。 この値がダッシュボードでどのように使われるかについて詳しくは、「Qualification 要素」をご覧ください。

```syntax
<xs:element name="LogoSubmissionIDList" type="tns:LogoSubmissionIDListType" minOccurs="0" maxOccurs="unbounded" />

<xs:complexType name="LogoSubmissionIDListType">
  <xs:sequence>
    <xs:element name="LogoSubmissionID" type="xs:integer"  maxOccurs="unbounded" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

### <a name="logosubmissionid-element"></a>LogoSubmissionID 要素

LogoSubmissionID 要素は、デバイスの個々のロゴ認定を指定します。 この値がダッシュボードでどのように使われるかについて詳しくは、「Qualification 要素」をご覧ください。

```syntax
<xs:element name="LogoSubmissionID" type="xs:integer"  maxOccurs="unbounded" />
```

複数の LogoSubmissionID 要素を使って、単一のデバイスの複数のロゴ認定を示すことができます。 ユーザーは、リスト内のデバイスに対してすべてのロゴ認定を指定する必要があります。 複数のロゴ認定が指定された例を次に示します。

```syntax
<LogoSubmissionIDList>
  <LogoSubmissionID>0000001</LogoSubmissionID>
  <LogoSubmissionID>0000002</LogoSubmissionID>
  <LogoSubmissionID>0000003</LogoSubmissionID>
</LogoSubmissionIDList>
```

### <a name="update-attribute"></a>update 属性

update 属性は、エクスペリエンスを更新するかどうかを指定します。 ダッシュボードは、この値に基づいてエクスペリエンスを更新します。つまり、update 属性が true の場合に、競合するパッケージを削除し、新しいパッケージをアップロードします。 update 属性が false の場合、ダッシュボードは、新しいエクスペリエンスを作成し、そこに新しいパッケージをアップロードします。

```syntax
<xs:attribute name="update" type="xs:boolean" use="required"/>
```

### <a name="bulkmetadatasubmission-xml-example"></a>BulkMetadataSubmission XML の例

以下の XML ドキュメントでは、BulkMetadataSubmission XML ドキュメントのコンポーネントが BulkMetadataSubmission XML スキーマを使って指定されています。

``` syntax
<BulkMetadataSubmission xmlns="http://schemas.microsoft.com/Windows/2010/08/MetadataSubmission/BulkMetadataSubmission">

  <Experience update="false">
    <ExperienceName>Test1</ExperienceName>
    <PackageList>
      <PackageFileName locale="en-us" preview ="false">
        XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.devicemanifest-ms
      </PackageFileName>
    </PackageList>
    <Qualification>Logo/IDDA</Qualification>
    <LogoSubmissionIDList>
      <LogoSubmissionID>XXXXXXX</LogoSubmissionID>
    </LogoSubmissionIDList>
  </Experience>

  <Experience update="false">
    <ExperienceName>Test2</ExperienceName>
    <PackageList>
      <PackageFileName locale="en-us" preview ="false">
        XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.devicemetadata-ms
      </PackageFileName>
    </PackageList>
    <Qualification>Logo/IDDA</Qualification>
    <LogoSubmissionIDList>
      <LogoSubmissionID>XXXXXXX</LogoSubmissionID>
    </LogoSubmissionIDList>
  </Experience>

  <Experience update="false">
    <ExperienceName>Test3</ExperienceName>
    <PackageList>
      <PackageFileName locale="en-us" preview="false">
        XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.devicemanifest-ms
      </PackageFileName>
    </PackageList>
    <Qualification>Logo/IDDA</Qualification>
    <LogoSubmissionIDList>
      <LogoSubmissionID>XXXXXXX</LogoSubmissionID>
    </LogoSubmissionIDList>
  </Experience>

  <Experience update="false">
    <ExperienceName>Test4</ExperienceName>
    <PackageList>
      <PackageFileName locale="en-us" preview="false">
        XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.devicemetadata-ms
      </PackageFileName>
    </PackageList>
    <Qualification>Logo/IDDA</Qualification>
    <LogoSubmissionIDList>
      <LogoSubmissionID>XXXXXXX</LogoSubmissionID>
    </LogoSubmissionIDList>
  </Experience>

  <Experience update="false">
    <ExperienceName>Test5</ExperienceName>
    <PackageList>
      <PackageFileName locale="en-us" preview="false">
        XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.devicemetadata-ms
      </PackageFileName>
    </PackageList>
    <Qualification>Logo/IDDA</Qualification>
    <LogoSubmissionIDList>
      <LogoSubmissionID>XXXXXXX</LogoSubmissionID>
    </LogoSubmissionIDList>
  </Experience>

</BulkMetadataSubmission>
```
