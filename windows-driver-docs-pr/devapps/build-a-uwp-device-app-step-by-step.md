---
title: UWP デバイス アプリを手順に従って構築する
description: このステップ バイ ステップ ガイドでは、Microsoft Visual Studio とデバイス メタデータ作成ウィザードを使用して UWP デバイス アプリをビルドする方法を詳しく説明しています。
ms.assetid: 2E3B47B6-1278-48EC-A530-64B8970A0142
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4d17a0fcee2989fa8d9879d613ec29ef5bbf3cd
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349307"
---
# <a name="span-iddevappsbuildawindowsstoredeviceappstep-by-stepspanbuild-a-uwp-device-app-step-by-step"></a><span id="devapps.build_a_windows_store_device_app_step-by-step"></span>ステップ バイ ステップの UWP デバイスのアプリをビルドします。


このステップ バイ ステップ ガイドでは、Microsoft Visual Studio とデバイス メタデータ作成ウィザードを使用して UWP デバイス アプリをビルドする方法を詳しく説明しています。 このプロセスに大まかな概要については、[構築 UWP デバイス アプリ](the-workflow.md)を参照してください。

UWP デバイスのアプリは、内部や周辺機器デバイスに対応するとして機能するデバイスの製造元が作成した UWP アプリの特別な種類です。 デバイス メタデータを使用すると、デバイス アプリは、特権操作を実行して、デバイスが接続されているときに自動的にインストールします。 UWP デバイスのアプリに関する詳細については、[満たす UWP デバイス アプリ](meet-uwp-device-apps.md)を参照してください。

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
<td align="left"><p><a href="step-1--create-a-uwp-device-app.md" data-raw-source="[Step 1: Create a UWP device app](step-1--create-a-uwp-device-app.md)">ステップ 1: UWP デバイス アプリを作成します。</a></p></td>
<td align="left"><p>このトピックでは、Visual Studio を使用して、UWP デバイス アプリを作成するための基本的なプロセスについて説明します。 すべての UWP デバイス アプリに共通するタスクについて説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="step-2--create-device-metadata.md" data-raw-source="[Step 2: Create device metadata](step-2--create-device-metadata.md)">手順 2:デバイス メタデータを作成します。</a></p></td>
<td align="left"><p>このトピックでは、使用する方法を説明します、<strong>デバイス メタデータの作成ウィザード</strong>UWP デバイス アプリをデバイスに関連付けられる新しいデバイス メタデータを作成します。 ウィザードで作成できますも、 <strong>StoreManfest.xml</strong>ファイルを次の手順で、アプリを追加する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="step-3--add-an-experience-id-to-the-app.md" data-raw-source="[Step 3: Add an experience ID to the app](step-3--add-an-experience-id-to-the-app.md)">手順 3:アプリに、エクスペリエンスの ID を追加します。</a></p></td>
<td align="left"><p>このトピックでは、UWP デバイスのアプリ エクスペリエンスの ID を追加する方法について説明します。 <em>ID エクスペリエンス</em>GUID は、デバイス メタデータ パッケージを一意に識別する; は必須では自動インストールの場合、アプリが構成されているかどうかは、<a href="uwp-device-apps-for-printers.md" data-raw-source="[UWP device apps for printers](uwp-device-apps-for-printers.md)">プリンター用の UWP デバイス アプリ</a>と<a href="uwp-device-apps-for-webcams.md" data-raw-source="[cameras](uwp-device-apps-for-webcams.md)">カメラ</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="step-4--test-device-metadata.md" data-raw-source="[Step 4: Test device metadata](step-4--test-device-metadata.md)">手順 4:テスト デバイス メタデータ</a></p></td>
<td align="left"><p>ここでは、テストする方法デバイス メタデータ UWP デバイス アプリをローカルで、Windows デベロッパー センター ダッシュ ボードに送信する前に説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="step-5--submit-the-app.md" data-raw-source="[Step 5: Submit the app](step-5--submit-the-app.md)">手順 5:アプリを送信します。</a></p></td>
<td align="left"><p>このトピックでは、Microsoft Store のダッシュ ボードに UWP デバイス アプリを送信する方法について説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="step-6--submit-device-metadata.md" data-raw-source="[Step 6: Submit device metadata](step-6--submit-device-metadata.md)">手順 6:デバイス メタデータを提出します。</a></p></td>
<td align="left"><p>このトピックでは、Windows デベロッパー センター ハードウェア ダッシュ ボードに UWP デバイス アプリのデバイス メタデータを送信する方法について説明します。</p></td>
</tr>
</tbody>
</table>

 

 

 





