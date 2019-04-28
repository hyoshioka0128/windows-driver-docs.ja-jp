---
title: センサーのアイコンを指定します。
description: センサーのアイコンを指定します。
ms.assetid: fe4a204f-befb-45d4-ad95-03b9e788e375
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b092fc0bbd75c7f4ba4cf037b7b98bb984c619af
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378570"
---
# <a name="specifying-a-sensor-icon"></a>センサーのアイコンを指定します。


センサー ドライバーには、一連のプラットフォームで定義されているアイコン、またはコントロール パネルの デバイスを表すためのカスタム アイコンのいずれかを指定できます。 特定のアイコンを指定するには、次の形式で DeviceIcon ドライバーの INX (または INF) 内のエントリ ファイルを作成します。

```c
DeviceIcon,,,,"<full path to DLL>,-<resource id>"
```

たとえば、光センサーのアイコンを指定するには、次のセクションを追加します。

```c

[DriverPropertiesSection]
DeviceIcon,,,,"%SystemRoot%\system32\sensorscpl.dll,-1008"
```

カスタム アイコンを指定するには、DLL のパスをアイコンを格納する DLL のパスに置き換えてし、リソース ID を適切な値に置き換えます。

かどうか、INX ファイルのドライバのプロパティ セクションに既に含まれません、追加する必要あります、`AddProperty`ディレクティブを`_Install.NT`セクション。 たとえば、時間のセンサーのサンプルでは、次のセクションを含めることが。

```c

[TimeSensor_Install.NT]
CopyFiles       = UMDriverCopy
AddProperty     = DriverPropertiesSection
```

INF ファイルでのデバイス プロパティの詳細については、次を参照してください。 [ **INF AddProperty ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addproperty-directive)します。

## <a name="related-topics"></a>関連トピック
[**センサー アイコン定数**](sensor-icon-constants.md)



