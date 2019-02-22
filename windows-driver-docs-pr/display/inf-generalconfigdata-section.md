---
title: INF GeneralConfigData セクション
description: INF GeneralConfigData セクション
ms.assetid: 49b00396-479f-471a-8c79-bb8ef33ebcaa
keywords:
- GeneralConfigData セクション
- Windows 2000 の WDK の INF ファイルを表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d374a91642d4eef7e36bd05e1b3472ef16735762
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557287"
---
# <a name="inf-generalconfigdata-section"></a>INF GeneralConfigData セクション


## <span id="ddk_inf_generalconfigdata_section_gg"></span><span id="DDK_INF_GENERALCONFIGDATA_SECTION_GG"></span>


ミニポート ドライバーでは、8 MB を超えるデバイスのメモリをマップする場合を**GeneralConfigData** INF ファイルのセクション。

```inf
[GeneralConfigData]

[MaximumDeviceMemoryConfiguration = n]
[MaximumNumberOfDevices = n]
```

次に**GeneralConfigData**エントリと値。

<span id="MaximumDeviceMemoryConfiguration_n"></span><span id="maximumdevicememoryconfiguration_n"></span><span id="MAXIMUMDEVICEMEMORYCONFIGURATION_N"></span>**MaximumDeviceMemoryConfiguration**=*n*  
ミニポート ドライバーは PCI によって列挙された 1 つのビデオ デバイスのシステム アドレス空間にマップしようとするデバイスのメモリのメガバイト数の最大数を指定します。 Windows では、ヒントとして値を使用して、特定数のシステム ページ テーブル エントリ (Pte) のマッピングを割り当てする必要があります。 このエントリを有効にするには、再起動が必要な場合があります。 デバイス マネージャーで、デバイスの状態をチェックして再起動する必要があるかどうかを指定できます。

<span id="MaximumNumberOfDevices_n"></span><span id="maximumnumberofdevices_n"></span><span id="MAXIMUMNUMBEROFDEVICES_N"></span>**MaximumNumberOfDevices**=*n*  
(PCI で列挙され、ミニポート ドライバーで駆動型) としてビデオ デバイスの数が、システムに存在する必要がありますを指定します。 かどうかにこのエントリを指定する必要がありますも指定する、 **MaximumDeviceMemoryConfiguration**エントリ。 このエントリを有効にするには、再起動が必要な場合があります。 デバイス マネージャーで、デバイスの状態をチェックして再起動する必要があるかどうかを指定できます。

1 つ以上のモニターをサポートする方法の詳細については、次を参照してください。[デュアル ビュー (Windows 2000 モデル) をサポートしている](supporting-dualview--windows-2000-model-.md)と[、ディスプレイ ドライバーでのマルチ モニター サポート](multiple-monitor-support-in-the-display-driver.md)します。









