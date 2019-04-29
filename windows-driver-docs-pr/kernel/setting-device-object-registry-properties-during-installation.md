---
title: インストール時のデバイス オブジェクト レジストリ プロパティの設定
description: インストール時のデバイス オブジェクト レジストリ プロパティの設定
ms.assetid: 29d40398-09b9-4e64-aa47-da229066bffd
keywords:
- デバイス オブジェクトの WDK カーネル、レジストリ
- レジストリの WDK デバイス オブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf560b528f01f4c22d04d8933a7e9342446da804
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385530"
---
# <a name="setting-device-object-registry-properties-during-installation"></a>インストール時のデバイス オブジェクト レジストリ プロパティの設定





インストール中にデバイス オブジェクトのプロパティを設定するには、プロパティを指定する INF ファイルを提供する必要があります。 デバイスまたはデバイス セットアップ クラスのいずれかのデバイス オブジェクトのプロパティを指定できます。

これらは、次のように指定されます。

-   個々 のデバイスのプロパティの設定、*追加レジストリ セクション*デバイス。 INF **AddReg**ディレクティブ内でのデバイスの*DDInstall*します。ハードウェア セクションを指定します、*追加レジストリ セクション*デバイス。

-   デバイス セットアップ クラスのプロパティの設定、*追加レジストリ セクション*のデバイス セットアップ クラス。 INF **AddReg**ディレクティブ内で、 **ClassInstall32**クラスは、指定のセクション、*追加レジストリ セクション*クラス。

内で、*追加レジストリ セクション*、個々 のデバイス オブジェクトのプロパティ設定を指定する次のキーワードを使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>キーワード</th>
<th>デバイス オブジェクトのプロパティ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DeviceType</strong></p></td>
<td><p>デバイスの種類</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceCharacteristics</strong></p></td>
<td><p>デバイスの特性</p></td>
</tr>
<tr class="odd">
<td><p><strong>[Exclusive]</strong></p></td>
<td><p>［排他］</p></td>
</tr>
<tr class="even">
<td><p><strong>セキュリティ</strong></p></td>
<td><p>セキュリティ記述子</p></td>
</tr>
</tbody>
</table>

 

これらのキーワードの使用に関する詳細については、次を参照してください。 [ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)します。

デバイス インストールの機能を使用して、ユーザー モード コンポーネントによって、設定を設定することができます。 詳細については、次を参照してください。[設定デバイス オブジェクト レジストリ インストール後にプロパティ](setting-device-object-registry-properties-after-installation.md)します。

 

 




