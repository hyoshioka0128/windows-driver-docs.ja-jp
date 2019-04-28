---
title: アセンブリの構成ファイル
description: アセンブリの構成ファイル
ms.assetid: 53BAC457-BB6A-44a8-AD8D-3B621F41A245
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43e45ed79f1bb9c33ade51578d80b83751308555
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383042"
---
# <a name="assembly-config-files"></a>アセンブリの構成ファイル


TAEF サポートは、アセンブリの構成ファイルをテストします。 構成ファイル、テスト アセンブリ +".config"と同じ名前が必要です。 指定されるテスト アセンブリがある場合**MyUnitTests.dll**、構成ファイルに名前を付ける**MyUnitTests.dll.config**します。

構成ファイルは、テスト アセンブリ ファイルと同じディレクトリに配置する必要があります。

## <a name="span-iddotnetcfspanspan-iddotnetcfspannet-configuration-files"></a><span id="dotnet_cf"></span><span id="DOTNET_CF"></span>.NET 構成ファイル


.NET 構成ファイルは、次の形式で XML ファイルです。

```cpp
<configuration>
    <appSettings>
        <add key="AssemblySetup" value="Assembly setup configuration information"/>
        <add key="ClassSetup" value="Class setup configuration information"/>
        <add key="TestSetup" value="Test setup configuration information"/>
        <add key="Test" value="Test configuration information"/>
    </appSettings>
</configuration>
```

構成ファイルは一連の名前/値のペア。

## <a name="span-idreadingcfspanspan-idreadingcfspanreading-the-configuration-file-from-your-tests"></a><span id="reading_cf"></span><span id="READING_CF"></span>テストから構成ファイルの読み取り


使用することができます、 **System.Configuration.ConfigurationManager**構成ファイルからデータを読み取るクラス。 以下に例を示します。

```cpp
NameValueCollection appStgs = ConfigurationManager.AppSettings;
Log.Comment(appStgs["AssemblySetup"]);
```

 

 





