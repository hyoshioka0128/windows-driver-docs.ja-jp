---
title: HID ドライバー
description: このセクションでは、ヒューマン インターフェイス デバイス (HID) について紹介します。 通常、これらは、人間がコンピューター システムの操作を直接制御するために使用するデバイスです。
ms.assetid: 19aefe5f-d82a-411f-86ab-5d1d53191524
keywords:
  - ポインティング デバイス WDK
  - 入力デバイス WDK
  - ヒューマン インターフェイス デバイス WDK
  - HID WDK
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# <a name="hid-drivers"></a>HID ドライバー


このセクションでは、ヒューマン インターフェイス デバイス (HID) について紹介します。 HID の概念の詳細については、公式の [HID の仕様](http://www.usb.org/developers/hidpage/HID1_11.pdf)をご覧ください。 

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
<td><p><a href="what-s-new-in-hid.md" data-raw-source="[What's New in HID](what-s-new-in-hid.md)">HID の新機能</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p><a href="introduction-to-hid-concepts.md" data-raw-source="[Introduction to HID Concepts](introduction-to-hid-concepts.md)">HID の概念の紹介</a></p></td>
<td><p>このセクションでは、ヒューマン インターフェイス デバイス (HID) について紹介します。 通常、これらは、人間がコンピューター システムの操作を直接制御するために使用するデバイスです。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hid-architecture.md" data-raw-source="[HID Architecture](hid-architecture.md)">HID のアーキテクチャ</a></p></td>
<td><p>Windows における HID ドライバー スタックのアーキテクチャは、<em>hidclass.sys</em> という名前のクラス ドライバー上に構築されています。</p></td>
</tr>
<tr class="even">
<td><p><a href="hid-clients-supported-in-windows.md" data-raw-source="[HID Clients Supported in Windows](hid-clients-supported-in-windows.md)">Windows でサポートされる HID クライアント</a></p></td>
<td><p>Windows では、次に示す最上位のコレクションがサポートされます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hid-transports-supported-in-windows.md" data-raw-source="[HID Transports Supported in Windows](hid-transports-supported-in-windows.md)">Windows でサポートされる HID トランスポート</a></p></td>
<td><p>Windows では、次のトランスポートがサポートされます。</p></td>
</tr>
<tr class="even">
<td><p><a href="hid-clients.md" data-raw-source="[HID Clients](hid-clients.md)">HID クライアント</a></p></td>
<td><p>HID クライアントは、HID API を使用して通信するドライバー、サービス、またはアプリケーションであり、多くの場合、特定の種類のデバイス (センサー、キーボード、マウスなど) を表します。 これらは、ハードウェア ID または特定の HID コレクションを通じてデバイスを識別し、HID API を通じて HID コレクションと通信します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hid-transports.md" data-raw-source="[HID Transports](hid-transports.md)">HID トランスポート</a></p></td>
<td><p>現在および以前のバージョンの Windows でサポートされる HID トランスポートの説明です。</p></td>
</tr>
<tr class="even">
<td><p><a href="non-hid-legacy-devices.md" data-raw-source="[Non-HID legacy devices](non-hid-legacy-devices.md)">非 HID のレガシ デバイス</a></p></td>
<td><p>このセクションでは、非 HID のキーボードとマウスに対応したドライバー、トランスポート、およびフィルター ドライバーについて説明します。 これらのデバイスは主に PS/2 トランスポートで実行されます。</p></td>
</tr>
</tbody>
</table>

 

 

 




