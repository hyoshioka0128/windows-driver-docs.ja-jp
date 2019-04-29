---
title: HID クライアント
description: HID クライアントは、ドライバー、サービスまたはアプリケーションを非表示に API を使用して通信し、多くの場合、特定の種類のデバイス (たとえば、センサー、キーボード、またはマウス) を表します。
ms.assetid: C97E1F63-0CA5-42F3-A139-48E830F2E2B7
keywords:
- HID クライアント
- ドライバー
- サービス
- HID API
- HID コレクション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01d8aff5e988702bd2b133ec0488632ee7cb312c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388812"
---
# <a name="hid-clients"></a>HID クライアント


HID クライアントは、HID API を使用して通信するドライバー、サービス、またはアプリケーションであり、多くの場合、特定の種類のデバイス (センサー、キーボード、マウスなど) を表します。 これらは、ハードウェア ID または特定の HID コレクションを通じてデバイスを識別し、HID API を通じて HID コレクションと通信します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="hid-usages.md" data-raw-source="[HID Usages](hid-usages.md)">HID の使用法</a></p></td>
<td><p><em>HID の使用法</em>HID コントロールとコントロールが実際に測定の使用目的を識別します。</p></td>
</tr>
<tr class="even">
<td><p><a href="hid-collections.md" data-raw-source="[HID Collections](hid-collections.md)">HID コレクション</a></p></td>
<td><p>A <em>HID コレクション</em>HID コントロールと、それぞれの意味のあるグループは、 <a href="hid-usages.md" data-raw-source="[HID usages](hid-usages.md)">HID の使用</a>します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="opening-hid-collections.md" data-raw-source="[Opening HID collections](opening-hid-collections.md)">HID のコレクションを開く</a></p></td>
<td><p>このセクションでは、HID クラス ドライバー、デバイスの HID コレクションを操作するには、(HIDClass) を使用した HID クライアントと通信する方法について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="handling-hid-reports.md" data-raw-source="[Handling HID Reports](handling-hid-reports.md)">HID レポートの処理</a></p></td>
<td><p>このセクションでは、ユーザー モード アプリケーションとカーネル モード ドライバーが処理に使用される機構をについて説明します<a href="introduction-to-hid-concepts.md" data-raw-source="[HID reports](introduction-to-hid-concepts.md)">HID レポート</a>します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="freeing-resources.md" data-raw-source="[Freeing Resources](freeing-resources.md)">リソースの解放</a></p></td>
<td><p>ユーザー モード アプリケーションと HID クライアントであるカーネル モード ドライバーは、不要になったリソースを解放常にする必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="installing-hid-clients.md" data-raw-source="[Installing HID clients](installing-hid-clients.md)">HID のクライアントをインストールします。</a></p></td>
<td><p>このセクションでは、Microsoft Windows に HIDClass デバイスをインストールする場合は、次の要件について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hidclass-hardware-ids-for-top-level-collections.md" data-raw-source="[HIDClass Hardware IDs for Top-Level Collections](hidclass-hardware-ids-for-top-level-collections.md)">最上位のコレクションの HIDClass ハードウェア Id</a></p></td>
<td><p>このセクションでは、ハードウェア、HID クラス ドライバーが最上位のコレクション用に生成する Id を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="keyboard-and-mouse-hid-client-drivers.md" data-raw-source="[Keyboard and mouse HID client drivers](keyboard-and-mouse-hid-client-drivers.md)">キーボードとマウスの HID クライアント ドライバー</a></p></td>
<td><p>このトピックでは、キーボードとマウスの HID クライアント ドライバーについて説明します。 キーボードとマウスは、HID Usage テーブルで標準化され、Windows オペレーティング システムで実装された HID クライアントの最初のセットを表します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sensor-hid-class-driver.md" data-raw-source="[Sensor HID class driver](sensor-hid-class-driver.md)">センサー HID クラス ドライバー</a></p></td>
<td><p>Windows 8 以降、Windows オペレーティング システムには、11 種類のセンサー HID トランスポートを使用して通信をサポートするインボックス センサー HID クラス ドライバー (SensorsHIDClassDriver.dll) が含まれています。</p></td>
</tr>
<tr class="even">
<td><p><a href="airplane-mode-radio-management.md" data-raw-source="[Airplane mode radio management](airplane-mode-radio-management.md)">機内モード無線管理</a></p></td>
<td><p>Windows 8 以降、Windows オペレーティング システムは、HID を介した機内モード無線管理コントロールのサポートを提供します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="display-brightness-control.md" data-raw-source="[Display brightness control](display-brightness-control.md)">ディスプレイの明るさコントロール</a></p></td>
<td><p>Windows 8 以降、標準化されたソリューションが追加されましたキーボード (外部またはラップトップで埋め込み)、hid のラップトップやタブレットの画面の明るさの制御を許可します。</p></td>
</tr>
</tbody>
</table>

 

 

 




