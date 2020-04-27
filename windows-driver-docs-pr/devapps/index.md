---
title: UWP デバイス アプリ
description: UWP デバイス アプリはデバイス コンパニオンであり、通常の UWP アプリを超える機能を備え、ファームウェアの更新などの特権操作を実行します
ms.assetid: fb64bad6-aa3d-4718-b62e-68da59a07ced
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
author: EliotSeattle
ms.openlocfilehash: 0e212c0b156b0ec25e87ccb52e3eebacec6d0a58
ms.sourcegitcommit: 988d100e4d3b218a59fdac034d39a1816d145c85
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "68995407"
---
# <a name="uwp-device-apps"></a>UWP デバイス アプリ


## <a name="span-idpurposespanpurpose"></a><span id="purpose"></span>目的


デバイス製造元は、デバイスのコンパニオンとして機能する UWP デバイス アプリを作成できます。 UWP デバイス アプリには、通常の UWP アプリより多くの機能を備え、ファームウェアの更新などの特権操作を実行できます。 さらに、UWP デバイス アプリは、自動再生から起動し (他のアプリよりも多くのデバイス上で)、デバイスが初めて接続されたときに自動的にインストールされ、Windows 8.1 および Windows 10 に組み込まれているプリンターやカメラのエクスペリエンスを拡張できます。

このセクションでは、UWP デバイス アプリの機能とデバイス製造元がそれらを作成する方法について説明します。 UWP デバイス アプリを初めて使用する場合は、[概要](getting-started.md)に関するページをご覧ください。

UWP モバイル ブロードバンド アプリに関する情報を探している場合は、「[Mobile Broadband](https://go.microsoft.com/fwlink/p/?LinkID=301754)」 (モバイル ブロードバンド) を参照してください。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


<table>  
<colgroup> <col width="50%" /> <col width="50%" /> </colgroup>  
<thead>  
<tr class="header">  
<th align="left">トピック</th>  
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="what-s-new.md" data-raw-source="[What's new](what-s-new.md)">新機能</a></p></td>
<td align="left"><p>このセクションでは、UWP デバイス アプリの新機能を簡単に説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="getting-started.md" data-raw-source="[Getting started](getting-started.md)">はじめに</a></p></td>
<td align="left"><p>UWP デバイス アプリのビルドを開始するには、ここから始めます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="build-a-uwp-device-app-step-by-step.md" data-raw-source="[Build a UWP device app step-by-step](build-a-uwp-device-app-step-by-step.md)">UWP デバイス アプリのビルド手順</a></p></td>
<td align="left"><p>このステップ バイ ステップ ガイドでは、Microsoft Visual Studio とデバイス メタデータ作成ウィザードを使用して UWP デバイス アプリをビルドする方法を詳しく説明しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="autoplay-for-uwp-device-apps.md" data-raw-source="[AutoPlay for UWP device apps](autoplay-for-uwp-device-apps.md)">UWP デバイス アプリの自動再生</a></p></td>
<td align="left"><p>このトピックでは、デバイス メタデータの作成ウィザードを使用して、自動再生を有効にする方法について説明しています。 アプリで自動再生のアクティブ化を処理する方法についても説明しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="device-sync-and-update-for-uwp-device-apps.md" data-raw-source="[Device sync and update for UWP device apps](device-sync-and-update-for-uwp-device-apps.md)">UWP デバイス アプリによるデバイスの同期と更新</a></p></td>
<td align="left"><p>Windows 8.1 では、UWP アプリは、デバイス バックグラウンド タスクを使用して、周辺機器上のデータを同期できます。 アプリがデバイス メタデータに関連付けられている場合、その UWP デバイス アプリは、デバイス バック グラウンド エージェントを使用して、ファームウェアの更新などのデバイスの更新を実行することもできます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="uwp-device-apps-for-printers.md" data-raw-source="[UWP device apps for printers](uwp-device-apps-for-printers.md)">プリンター用の UWP デバイス アプリ</a></p></td>
<td align="left"><p>このセクションでは、プリンター用の UWP デバイス アプリを紹介します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="uwp-device-apps-for-webcams.md" data-raw-source="[UWP device apps for cameras](uwp-device-apps-for-webcams.md)">カメラ用の UWP デバイス アプリ</a></p></td>
<td align="left"><p>このセクションでは、カメラ用の UWP デバイス アプリを紹介します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="uwp-device-apps-for-specialized-devices.md" data-raw-source="[UWP device apps for internal devices](uwp-device-apps-for-specialized-devices.md)">内部デバイス用の UWP デバイス アプリ</a></p></td>
<td align="left"><p>このトピックでは、UWP デバイス アプリが内部デバイスにアクセスできる方法について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="auto-install-for-uwp-device-apps.md" data-raw-source="[Automatic installation for UWP device apps](auto-install-for-uwp-device-apps.md)">UWP デバイス アプリの自動インストール</a></p></td>
<td align="left"><p>このトピックでは、自動インストールのしくみとアプリ、メタデータ、およびドライバーの更新およびアンインストール方法について説明します。</p></td>
</tr>
</tr>
<tr class="even">
<td align="left"><p><a href="hardware-support-app--hsa--steps-for-driver-developers.md" data-raw-source="[Hardware Support App (HSA): Steps for Driver Developers](hardware-support-app--hsa--steps-for-driver-developers.md)">ハードウェア サポート アプリ (HSA):ドライバー開発者向け手順</a></p></td>
<td align="left"><p>このトピックでは、ドライバーとユニバーサル Windows プラットフォーム (UWP) アプリを関連付けるドライバー開発者向けの手順を説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="hardware-support-app--hsa--steps-for-app-developers.md" data-raw-source="[Hardware Support App (HSA): Steps for App Developers](hardware-support-app--hsa--steps-for-app-developers.md)">ハードウェア サポート アプリ (HSA):アプリ開発者向け手順</a></p></td>
<td align="left"><p>このトピックでは、ユニバーサル Windows プラットフォーム (UWP) アプリとユニバーサル Windows ドライバーを関連付けるアプリ開発者向けの手順を説明します。</p></td>
</tr>
</tbody>
</table>

 

 

 





