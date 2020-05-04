---
title: INF DDInstall.LogConfigOverride セクション
description: DDInstall. LogConfigOverride セクションは、ハードウェアリソース要件を上書きする上書き構成を作成するために使用されます。
ms.assetid: 7ee8d221-7cdb-4373-aa8b-2d5164f6a636
keywords:
- INF DDInstall. LogConfigOverride セクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DDInstall.LogConfigOverride Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71032e8e8fb8a3e8b4e75ad24c987664b41ec45d
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223232"
---
# <a name="inf-ddinstalllogconfigoverride-section"></a>INF DDInstall.LogConfigOverride セクション


**注**  ユニバーサルまたはモバイルのドライバーパッケージを作成する場合、このセクションは無効です。 「[ユニバーサル INF ファイルの使用」を](using-a-universal-inf-file.md)参照してください。

 

<em>Ddinstall</em>**。LogConfigOverride**セクションは、[上書き構成](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources#logical-configuration-types-for-resource-requirements-lists)を作成するために使用されます。これは、プラグアンドプレイデバイスのバスドライバーが報告するハードウェアリソース要件を上書きします。

```inf
[install-section-name.LogConfigOverride] |
[install-section-name.nt.LogConfigOverride] |
[install-section-name.ntx86.LogConfigOverride] |
[install-section-name.ntarm.LogConfigOverride] | (Windows 8 and later versions of Windows)
[install-section-name.ntarm64.LogConfigOverride] | (Windows 10 version 1709 and later versions of Windows)
[install-section-name.ntia64.LogConfigOverride] |  (Windows XP and later versions of Windows)
[install-section-name.ntamd64.LogConfigOverride]  (Windows XP and later versions of Windows)
 
LogConfig=log-config-section[,log-config-section]...] 
```

## <a name="entries"></a>エントリ


<em>Ddinstall</em>で使用されるセクションのエントリと値 **。LogConfigOverride**セクションは、 [**INF logconfig ディレクティブ**](inf-logconfig-directive.md)によって参照される*ログ構成セクション*内で指定されます。

<a name="remarks"></a>解説
-------

プラグアンドプレイデバイスの*ログ構成セクション*で指定されている構成データは、優先ハードウェアリソース構成ですが、絶対的な要件ではありません。 指定されたハードウェアリソース構成データの一部またはすべてが、デバイスの基になるバスドライバーで受け入れられない可能性があります。 この場合、デバイスドライバーには、最初にバスドライバーによって報告されたハードウェアリソースが割り当てられます。

<a name="examples"></a>例
--------

次の例は、 <em>Ddinstall</em>を示して**います。LogConfigOverride**セクションと、PCMCIA デバイスの対応する*ログ構成セクション*。

```inf
[XYZDevice.LogConfigOverride]
LogConfig = XYZDevice.Override0

[XYZDevice.Override0]
IOConfig=2f8-2ff
IOConfig=20@100-FFFF%FFE0
IRQConfig=3,4,5,7,9,10,11
MemConfig=4000@0-FFFFFFFF%FFFFC000
PcCardConfig=41:100000(W)
```

*ログ構成セクション*で指定されているハードウェアリソース構成のデータ値の詳細については、「 [**INF logconfig ディレクティブ**](inf-logconfig-directive.md)」を参照してください。

## <a name="see-also"></a>関連項目


[***DDInstall***](inf-ddinstall-section.md)

 

 






