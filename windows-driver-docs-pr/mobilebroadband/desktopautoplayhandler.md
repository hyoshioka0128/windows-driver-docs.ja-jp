---
title: DesktopAutoplayHandler
description: DesktopAutoplayHandler
ms.assetid: e1a07580-36dd-4618-b522-3f7605c9b87b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 578f2071d1847814bc878de55e704875cf6f9f80
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323623"
---
# <a name="desktopautoplayhandler"></a>DesktopAutoplayHandler

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

DesktopAutoplayHandler 要素は、デバイスが接続されていて、既定の動作が設定されていない場合に、推奨される自動再生アクションとして表示されるデスクトップアプリを指定します。 自動再生イベントは、ユーザーがデバイスに接続するたびに発生します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<DesktopAutoplayHandler>
  text
</DesktopAutoplayHandler>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


属性はありません。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


自動再生イベントを処理するデスクトップアプリを示す文字列。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子要素


子要素はありません。

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
<td><p><a href="windowsinfo.md" data-raw-source="[WindowsInfo](windowsinfo.md)">WindowsInfo</a></p></td>
<td><p><a href="windowsinfo-xml-schema.md" data-raw-source="[WindowsInfo XML schema](windowsinfo-xml-schema.md)">Windowsinfo XML スキーマ</a>の親要素。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="DesktopAutoplayHandler" type="xs:string" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


デスクトップアプリを設定するときに、DesktopAutoplayHandler 要素でデスクトップの自動再生ハンドラー文字列を指定します。 次のレジストリキーの下に登録されているハンドラーサブキーの名前から文字列を取得できます。

``` syntax
HKLM\Software\Microsoft\Windows\CurrentVersion\Explorer\AutoplayHandlers\Handlers
```

DesktopAutoplayHandler 要素は省略可能です。

 

 





