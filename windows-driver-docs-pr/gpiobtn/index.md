---
title: ハードウェア通知設計ガイド
description: 主要なボタン (電源、Windows、ボリューム、回転ロック) とその他のインジケーターの標準化された方法でのサポート、および関連する Windows Engineering Guidance (WEG) について説明します。
ms.assetid: E18DAA6C-C64D-40B3-A112-682A935655D0
ms.date: 06/16/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 89af40e81bf59ba0f68b4e28e40071aed167daeb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323430"
---
# <a name="hardware-notifications-design-guide"></a>ハードウェア通知設計ガイド


主要なボタン (電源、Windows、ボリューム、回転ロック) とその他のインジケーターの標準化された方法でのサポート、および関連する Windows Engineering Guidance (WEG) について説明します。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="gpio-buttons-and-indicators-implementation-guide-for-windows-8-1.md" data-raw-source="[GPIO buttons and indicators implementation guide](gpio-buttons-and-indicators-implementation-guide-for-windows-8-1.md)">GPIO のボタンおよびインジケーター実装ガイド</a></p></td>
<td align="left"><p>Windows 8 では、HID ミニポート クラス ドライバーを使用して、汎用 I/O (GPIO) のボタンとインジケーターのサポートが導入されていました。 その目的は、主要なボタン (電源、Windows、ボリューム、回転ロック) の標準化された方法でのサポート、および関連する Windows Engineering Guidance (WEG) を提供することでした。 Windows 8.1 では、エンド ツー エンドのユーザー エクスペリエンスの品質の向上および革新的なさまざまなフォーム ファクター間での動作の統一に重点を置いています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="gpio-buttons-and-indicators-supplemental-certification-testing-for-windows-8-1.md" data-raw-source="[GPIO buttons and indicators supplemental testing](gpio-buttons-and-indicators-supplemental-certification-testing-for-windows-8-1.md)">GPIO のボタンおよびインジケーターの補足的なテスト</a></p></td>
<td align="left"><p>このトピックでは、さまざまなフォーム ファクターに最適なユーザー エクスペリエンスを確保するための、ハードウェアのボタンとインジケーターに対する Windows 8.1 のテスト シナリオについて説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="hardware-notifications-support.md" data-raw-source="[Hardware notifications support](hardware-notifications-support.md)">ハードウェア通知のサポート</a></p></td>
<td align="left"><p>Windows 10 バージョン 1709 には、通知コンポーネント (LED、振動のメカニズムなど) のハードウェアに依存しないサポート用のインフラストラクチャが用意されています。 このサポートは、クライアント ドライバーの迅速な開発を可能にするハードウェア通知コンポーネント専用のカーネルモード ドライバー フレームワーク (KMDF) クラスの拡張を導入することで提供されます。 KMDF クラスの拡張は、本質的には、特定のクラスのデバイス用に定義された機能セットを提供する KMDF ドライバーであり、Windows Driver Model (WDM) 内のポート ドライバーと同様です。 このセクションでは、ハードウェア通知クラスの拡張のアーキテクチャの概要を示します。 KMDF の詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-to-develop-a-driver" data-raw-source="[Using WDF to Develop a Driver](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-to-develop-a-driver)">Using WDF to Develop a Driver (WDF を使用したドライバーの開発)</a>」をご覧ください。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[ハードウェア通知リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn789336)



