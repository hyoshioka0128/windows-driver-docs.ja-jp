---
title: AutoplayHandler
description: AutoplayHandler
ms.assetid: 0ee7ac9b-7c1a-4267-b718-ba110ef5b12d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53a0041d692a7208998922bef0bc32ffaabacfc3
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323636"
---
# <a name="autoplayhandler"></a>AutoplayHandler

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

AutoplayHandler 要素は、ユーザーがデバイスに接続するときに推奨される自動再生アクションとして表示される UWP デバイスアプリを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<AutoplayHandler>
  child elements
</AutoplayHandler>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


属性はありません。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子要素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="packageidentity.md" data-raw-source="[PackageIdentity](packageidentity.md)">PackageIdentity</a></p></td>
<td><p>アプリのパッケージ id (名前と発行元) を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="application-windowsinfo-v2.md" data-raw-source="[Application](application-windowsinfo-v2.md)">アプリケーション</a></p></td>
<td><p>アプリのアプリケーション ID を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="verb.md" data-raw-source="[Verb](verb.md)">助動詞</a></p></td>
<td><p>アプリによって登録される動詞を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="autoplaytype.md" data-raw-source="[AutoplayType](autoplaytype.md)">AutoplayType</a></p></td>
<td><p>自動再生イベントがデバイスイベントとコンテンツイベントのどちらであるかを指定します。 自動再生では、デバイスの種類が決定され、ボリューム以外のデバイスの場合はデバイスイベント、ボリュームデバイスの場合はコンテンツイベントが発生します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="enableautoplayforregisteredapps.md" data-raw-source="[EnableAutoPlayForRegisteredApps](enableautoplayforregisteredapps.md)">EnableAutoPlayForRegisteredApps</a></p></td>
<td><p>登録済みアプリで自動再生を有効にするかどうかを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idparent_elementsspanspan-idparent_elementsspanspan-idparent_elementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>親要素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="launchapplicationondeviceconnect.md" data-raw-source="[LaunchApplicationOnDeviceConnect](launchapplicationondeviceconnect.md)">LaunchApplicationOnDeviceConnect</a></p></td>
<td><p>ユーザーがデバイスに接続したときに推奨される自動再生操作として表示するアプリを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
      <xs:element name="AutoplayHandler" type="tns:AutoplayHandlerType" />

  <xs:complexType name="AutoplayHandlerType">
    <xs:sequence>
      <xs:element name="PackageIdentity" type="tns:PackageIdentityType" />
      <xs:element name="Application" type="tns:ApplicationType" />
      <xs:element name="Verb" type="tns:VerbType" />
      <xs:element name="AutoplayType" type="tns:AutoplayTypeType" />
      <xs:element name="EnableAutoPlayForRegisteredApps" type ="xs:boolean" default="false" minOccurs="0" />
      <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
    </xs:sequence>
  </xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


-   [PackageIdentity](packageidentity.md)要素と[application](application-windowsinfo-v2.md)要素の構造は、アプリケーションマニフェスト構造と同じであるため、アプリケーションのマニフェストから要素をコピーします。

-   デバイスメタデータに AutoplayHandler 要素を含めるだけでなく、指定された UWP デバイスアプリも、イベントのアプリケーションマニフェストに宣言を追加することによって、自動再生イベントに登録する必要があります。 自動再生は、アプリの宣言を認識し、そのイベントに応答するためにユーザーが実行できるアクションのリストに含めます。

-   デバイスのインストールの一部としてダウンロードされるのは、DeviceCompanionApplications ファイルの[値に記載されているパッケージだけです](devicecompanionapplications.md)。 [LaunchApplicationOnDeviceConnect](launchapplicationondeviceconnect.md)要素の値が別のパッケージからのものである場合、Windows は実際にユーザーのデバイス上にあるかどうかを認識しません。 推奨されるアプリケーションがユーザーのデバイスにない場合は、ユーザーに選択内容が表示されません。

-   アプリケーションが[DeviceCompanionApplications](devicecompanionapplications.md)エントリと同じ場合でも、自動再生リストに表示されないことがあります。 ユーザーがインターネットに接続されていない場合、またはコンパニオンアプリケーションのダウンロードに失敗した場合は、一覧に表示されません。 ただし、ユーザーがアプリケーションを取得すると、次にデバイスを接続したときに [新しいオプションを利用可能] というダイアログボックスが表示されます。

AutoplayHandler 要素は省略可能です。

 

 





