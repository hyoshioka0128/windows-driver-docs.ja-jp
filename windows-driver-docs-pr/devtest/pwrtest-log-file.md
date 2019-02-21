---
title: PwrTest ログ ファイル
description: PwrTest ログ ファイル
ms.assetid: f4782b27-25e0-4ec3-bf0b-82a614815f90
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1dd168fbde39d015ae0a986486409acf8a58194
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550622"
---
# <a name="pwrtest-log-file"></a>PwrTest ログ ファイル


PwrTest は、さまざまな形式で複数の同時ログ出力をサポートしています: .log (プレーン テキスト)、.xml (形式は各シナリオは異なります)、.wtl (WTTLog) および .etl (ETW トレース)。 既定では、PwrTest は pwrtestlog という名前のログ ファイルを生成します。\*. 使用することができます、 **/ln:**<em>名前</em>ログ名を変更するオプション。 これらのファイルが、既定では、現在のディレクトリに生成されます。 使用することができます、 **/lf:**<em>フォルダー</em>出力場所を変更するオプション。

WTTLog ファイルの形式は WTTLog インターフェイスを使用するすべての Microsoft Windows Driver Kit (WDK) ツールに共通です。 PwrTest を WTTLog がインストールされていないコンピューターで実行する場合、PwrTest は .wtl (WTTLog) ログ ファイルを生成しません。

PwrTest .xml のログ ファイル (pwrtestlog.xml) は、実行される特定のシナリオについての情報を提供します。 PwrTest .xml のすべてのログ ファイルは、次のルート要素とヘッダーがあります。

```XML
<PwrTestLog date="today&#39;s date" time="beginning time" filename = "logfile path">
  <SystemInformation>
    <ComputerName></ComputerName>
    <OSBuildNumber></OSBuildNumber>
    <SystemManufacturer></SystemManufacturer>
    <SystemProductName></SystemProductName>
    <BIOSVersion></BIOSVersion>
    <BIOSReleaseDate></BIOSReleaseDate>
    <ProcessorCount></ProcessorCount>
    <ProcessorPackageCount></ProcessorPackageCount>
  </SystemInformation>

  ... 
  scenario tags and data
  ...

</PwrTestLog>
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest 構文](pwrtest-syntax.md)

 

 






