---
title: INF DDInstall.LogConfigOverride セクション
description: DDInstall.LogConfigOverride のセクションでは、ハードウェア リソース要件を上書きする上書き構成の作成に使用されます。
ms.assetid: 7ee8d221-7cdb-4373-aa8b-2d5164f6a636
keywords:
- INF DDInstall.LogConfigOverride セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DDInstall.LogConfigOverride Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e3f12cdd81e3b6348db16a6d10c282bfeec4dd6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385908"
---
# <a name="inf-ddinstalllogconfigoverride-section"></a>INF DDInstall.LogConfigOverride セクション


**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このセクションが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

<em>DDInstall</em>**します。LogConfigOverride**セクションを使用して作成、[構成をオーバーライドする](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources#logical-configuration-types-for-resource-requirements-lists)、バス ドライバーのプラグ アンド プレイ デバイスの報告されたハードウェア リソース要件をオーバーライドします。

```ini
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


セクションのエントリとで使用される値<em>DDInstall</em>**します。LogConfigOverride**内のセクションに指定された*ログ-構成-セクション*によって参照される[ **INF LogConfig ディレクティブ**](inf-logconfig-directive.md)します。

<a name="remarks"></a>注釈
-------

指定されている構成データ、*ログの構成 セクションで*のプラグ アンド プレイ デバイスが推奨されるハードウェア リソースの構成が、絶対要件ではありません。 指定されたハードウェア リソースの構成データの一部またはすべてをデバイスの基になるバス ドライバーで受け入れられません可能性があります。 このような状況では、デバイス ドライバーには、バス ドライバーによって報告された最初のハードウェア リソースが割り当てられます。

<a name="examples"></a>例
--------

次の例は、 <em>DDInstall</em>**します。LogConfigOverride**セクションと、対応する*ログの構成 セクションで*PCMCIA デバイス。

```ini
[XYZDevice.LogConfigOverride]
LogConfig = XYZDevice.Override0

[XYZDevice.Override0]
IOConfig=2f8-2ff
IOConfig=20@100-FFFF%FFE0
IRQConfig=3,4,5,7,9,10,11
MemConfig=4000@0-FFFFFFFF%FFFFC000
PcCardConfig=41:100000(W)
```

指定されているハードウェア リソースの構成データ値の詳細については、*ログの構成 セクションで*を参照してください[ **INF LogConfig ディレクティブ**](inf-logconfig-directive.md)します。

## <a name="see-also"></a>関連項目


[***DDInstall***](inf-ddinstall-section.md)

 

 






