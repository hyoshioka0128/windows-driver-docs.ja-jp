---
title: モニター プロファイル
description: モニター プロファイル
ms.assetid: aede7ada-3826-40a4-8b37-18ae242eea77
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、色の管理
- Windows 2000 の WDK の色の管理を表示します。
- ディスプレイ ドライバー WDK Windows 2000 では、プロファイルを監視します。
- モニターの WDK Windows 2000 のプロファイルの表示
- Windows 2000 の WDK のデバイス プロファイルを表示します。
- 色空間 WDK Windows 2000 の表示
- 広色域 WDK Windows 2000 の表示
- デバイス非依存の色空間 WDK Windows 2000 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75530936648e2086c9f10b02e8686c30993bc442
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362093"
---
# <a name="monitor-profiles"></a>モニター プロファイル


## <span id="ddk_monitor_profiles_gg"></span><span id="DDK_MONITOR_PROFILES_GG"></span>


A*プロファイルを監視*は色の管理に使用するデバイス プロファイルの一種です。 このプロファイルには、モニターの色を変換する方法に関する情報が含まれています。*領域の色*と*広色域*デバイス非依存の色領域の色にします。 任意のユーザー モード アプリケーションは、セットアップ プログラムまたはグラフィックス機能を備えた、ワード プロセッサがモニターのプロファイルを使用するなど、提供を*ICM*有効になっているアプリケーションがプロファイルの形式の情報を持っているとします。

サード パーティ製ツールを使用してカスタムのモニター プロファイルを作成できますが、Windows 2000 およびそれ以降のオペレーティング システム バージョンに付属のモニター プロファイルのいずれかを使用することができます。 これらのプロファイルは、次の表で説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Profile</th>
<th align="left">モニターの特性</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>mnB22G15.icm</p></td>
<td align="left"><p>B22 発光体、ガンマ 1.5</p></td>
</tr>
<tr class="even">
<td align="left"><p>mnB22G18.icm</p></td>
<td align="left"><p>B22 発光体、ガンマ 1.8</p></td>
</tr>
<tr class="odd">
<td align="left"><p>mnB22G21.icm</p></td>
<td align="left"><p>B22 発光体は、ガンマ 2.1 です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>mnEBUG15.icm</p></td>
<td align="left"><p>EBU 発光体、ガンマ 1.5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>mnEBUG18.icm</p></td>
<td align="left"><p>EBU 発光体、ガンマ 1.8</p></td>
</tr>
<tr class="even">
<td align="left"><p>mnEBUB21.icm</p></td>
<td align="left"><p>EBU 発光体、ガンマ 2.1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>mnP22G15.icm</p></td>
<td align="left"><p>P22 発光体、ガンマ 1.5</p></td>
</tr>
<tr class="even">
<td align="left"><p>mnP22G18.icm</p></td>
<td align="left"><p>P22 発光体、ガンマ 1.8</p></td>
</tr>
<tr class="odd">
<td align="left"><p>mnP22G21.icm</p></td>
<td align="left"><p>P22 発光体、ガンマ 2.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>互換性のある 9300 K G2.2.icm をひし形</p></td>
<td align="left"><p>9300Â ° ケルビン ホワイト ポイント、ガンマ値 2.2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>日立互換性のある 9300 K G2.2.icm</p></td>
<td align="left"><p>9300Â ° ケルビン ホワイト ポイント、ガンマ値 2.2</p></td>
</tr>
<tr class="even">
<td align="left"><p>NEC 互換性のある 9300 K G2.2.icm</p></td>
<td align="left"><p>9300Â ° ケルビン ホワイト ポイント、ガンマ値 2.2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>トリニトロン互換性のある 9300 K G2.2.icm</p></td>
<td align="left"><p>9300Â ° ケルビン ホワイト ポイント、ガンマ値 2.2</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idinstallingamonitorprofilespanspan-idinstallingamonitorprofilespanspan-idinstallingamonitorprofilespaninstalling-a-monitor-profile"></a><span id="Installing_a_Monitor_Profile"></span><span id="installing_a_monitor_profile"></span><span id="INSTALLING_A_MONITOR_PROFILE"></span>モニターのプロファイルをインストールします。

ユーザーは、3 つの方法で、モニターのプロファイルをインストールできます。

1.  Windows エクスプ ローラーで、プロファイルを選択します。、、名を右クリックおよびクリック**プロファイルのインストール**します。

2.  プロファイルを参照してください、[モニター INF ファイル](monitor-inf-file-sections.md)します。

3.  ハードコードされたアプリケーションでプロファイルのパスとファイルの名前します。

プロファイルの監視の既定のディレクトリが変更される可能性があるために、ハード コーディングするプロファイルのパスとファイル名はお勧めしません。

### <a name="span-idusingamonitorprofilespanspan-idusingamonitorprofilespanspan-idusingamonitorprofilespanusing-a-monitor-profile"></a><span id="Using_a_Monitor_Profile"></span><span id="using_a_monitor_profile"></span><span id="USING_A_MONITOR_PROFILE"></span>プロファイル モニターを使用します。

プリンターのプロファイルとは異なり、モニターのプロファイルでは、出力デバイスとアプリケーション間のごくわずかな通信をサポートします。 たとえば、ユーザーは、ビデオのバッファーでガンマごとの傾斜増加を変更する場合、モニターのプロファイルは通知されませんこのような変更が発生したこと。 この場合、icm が有効になっている、2 つの色の修正に適用されます、イメージが表示されたら、前に、次の一連の手順で示すように。

1.  アプリケーションが開き、イメージを操作します。

2.  アプリケーションにより、ICM、GDI ICM の Win32 関数の呼び出しなど**SetICMMode**します。 (詳細については、Microsoft Windows SDK を参照してください)。

3.  アプリケーションでは、Win32 の GDI にイメージを送信します。

4.  ICM が有効になっている場合、Win32 GDI は、イメージの色を変換するモニターのプロファイルを使用します。

5.  Win32 GDI では、カーネル モードの GDI にイメージを送信します。

6.  カーネル モードの GDI では、画像がビット深度、解決、およびハーフトーンとして、デバイス コンテキスト (DC) のようなデバイス特性に基づき、ディスプレイ ドライバーが書式設定します。

7.  ディスプレイ ドライバー (またはビデオ ハードウェア) は、イメージのガンマ補正を実行します。

 

 





