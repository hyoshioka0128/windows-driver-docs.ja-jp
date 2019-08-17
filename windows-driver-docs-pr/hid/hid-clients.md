---
title: HID クライアントの概要
description: HID クライアントは、HID API を使用して通信するドライバー、サービス、またはアプリケーションで、多くの場合、特定の種類のデバイス (センサー、キーボード、マウスなど) を表します。
ms.assetid: C97E1F63-0CA5-42F3-A139-48E830F2E2B7
keywords:
- HID クライアント
- ドライバー
- サービス
- HID API
- HID コレクション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee66f22cf9113910bd9acb908418469638e5a8ca
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565628"
---
# <a name="hid-clients-overview"></a>HID クライアントの概要


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
<td><p><a href="hid-usages.md" data-raw-source="[HID Usages](hid-usages.md)">HID の使用</a></p></td>
<td><p><em>Hid usage</em>は、hid コントロールの使用目的、およびコントロールが実際にどのように測定するかを特定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="hid-collections.md" data-raw-source="[HID Collections](hid-collections.md)">HID コレクション</a></p></td>
<td><p><em>Hid コレクション</em>は、hid コントロールとそれぞれの<a href="hid-usages.md" data-raw-source="[HID usages](hid-usages.md)">hid 使用法</a>を意味的にグループ化したものです。</p></td>
</tr>
<tr class="odd">
<td><p><a href="opening-hid-collections.md" data-raw-source="[Opening HID collections](opening-hid-collections.md)">HID コレクションを開く</a></p></td>
<td><p>このセクションでは、hid クライアントが HID クラスドライバー (HIDClass) と通信して、デバイスの HID コレクションを操作する方法について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="handling-hid-reports.md" data-raw-source="[Handling HID Reports](handling-hid-reports.md)">HID レポートの処理</a></p></td>
<td><p>このセクションでは、ユーザーモードアプリケーションとカーネルモードドライバーが<a href="introduction-to-hid-concepts.md" data-raw-source="[HID reports](introduction-to-hid-concepts.md)">HID レポート</a>の処理に使用するメカニズムについて説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="freeing-resources.md" data-raw-source="[Freeing Resources](freeing-resources.md)">リソースを解放する</a></p></td>
<td><p>HID クライアントであるユーザーモードアプリケーションとカーネルモードドライバーは、不要になったリソースを常に解放する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="installing-hid-clients.md" data-raw-source="[Installing HID clients](installing-hid-clients.md)">HID クライアントのインストール</a></p></td>
<td><p>このセクションでは、Microsoft Windows で HIDClass デバイスをインストールするための次の要件について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hidclass-hardware-ids-for-top-level-collections.md" data-raw-source="[HIDClass Hardware IDs for Top-Level Collections](hidclass-hardware-ids-for-top-level-collections.md)">最上位レベルのコレクションのハードウェア Id を HIDClass する</a></p></td>
<td><p>このセクションでは、HID クラスドライバーが最上位レベルのコレクションに対して生成するハードウェア Id を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="keyboard-and-mouse-hid-client-drivers.md" data-raw-source="[Keyboard and mouse HID client drivers](keyboard-and-mouse-hid-client-drivers.md)">キーボードとマウスの HID クライアントドライバー</a></p></td>
<td><p>このトピックでは、キーボードとマウスの HID クライアントドライバーについて説明します。 キーボードとマウスは、HID の使用表で標準化され、Windows オペレーティングシステムに実装されている最初の HID クライアントのセットを表します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sensor-hid-class-driver.md" data-raw-source="[Sensor HID class driver](sensor-hid-class-driver.md)">センサー HID クラスドライバー</a></p></td>
<td><p>Windows 8 以降、Windows オペレーティングシステムには、HID トランスポートを使用して通信する11種類のセンサーをサポートするインボックスセンサー HID クラスドライバー (SensorsHIDClassDriver .dll) が含まれています。</p></td>
</tr>
<tr class="even">
<td><p><a href="airplane-mode-radio-management.md" data-raw-source="[Airplane mode radio management](airplane-mode-radio-management.md)">航空機モードのラジオ管理</a></p></td>
<td><p>Windows 8 以降では、Windows オペレーティングシステムは、航空機モードのラジオ管理コントロール用に HID を介してサポートを提供します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="display-brightness-control.md" data-raw-source="[Display brightness control](display-brightness-control.md)">画面の明るさの調整</a></p></td>
<td><p>Windows 8 以降では、標準のソリューションが追加されました。キーボードを使用して (外付けまたはノート pc に内蔵)、HID を通じてノート pc やタブレットの画面の明るさを制御します。</p></td>
</tr>
</tbody>
</table>

 

 

 




