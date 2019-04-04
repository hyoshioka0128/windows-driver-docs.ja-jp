---
title: デバイス メタデータのエラー コード
description: デバイス メタデータのエラー コード
ms.assetid: 7ca3b9d3-8e7d-4421-affa-bddea2d4c262
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0724edeae8b219dd267367712229b3a9158f87e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549841"
---
# <a name="device-metadata-error-codes"></a>デバイス メタデータのエラー コード


以降、Windows 7 オペレーティング システムでは、次のエラー コードのダウンロードに関連するイベント内のログと、デバイス メタデータ パッケージの処理します。 これらのイベントは Event Tracing for Windows (ETW) サービスによって管理され、イベント ビューアーを使用して表示することができます。 これらのイベントに関する詳細については、[デバッグ デバイス メタデータ パッケージを使用してイベント ビューアー](debugging-device-metadata-packages-by-using-event-viewer.md)を参照してください。

<a href="" id="windows-metadata-and-internet-services--wmis--errors--200000xx-"></a>Windows メタデータとインターネット サービス (WMIS) エラー (200000xx)  
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エラー コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>20000021</p></td>
<td align="left"><p>要求では、デバイス メタデータの要求は含まれません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>20000022</p></td>
<td align="left"><p>要求のバッチ サイズが最大許容値を超えています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>20000023</p></td>
<td align="left"><p>ロケールの値が無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>20000024</p></td>
<td align="left"><p>要求に有効なヘッダー情報が含まれていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>20000025</p></td>
<td align="left"><p>要求の形式が無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>20000031</p></td>
<td align="left"><p>要求を処理するときに、サービス側でエラーが発生しました。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="device-metadata-retrieval-client--dmrc--errors--0x400000xx-"></a>デバイス メタデータの取得 (DMRC) クライアント エラー (0x400000xx)  
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エラー コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>40000011</p></td>
<td align="left"><p>ローカルのメタデータ キャッシュはありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>40000012</p></td>
<td align="left"><p>ローカルのメタデータ キャッシュ内の構造 (フォルダー) が正しくありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>40000021</p></td>
<td align="left"><p>ローカルのメタデータ ストアはありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>40000022</p></td>
<td align="left"><p>ローカル メタデータ ストアには、(フォルダー) 構造体が壊れています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>40000031</p></td>
<td align="left"><p>DMRC インデックスのデータがありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>40000032</p></td>
<td align="left"><p>DMRC インデックス データが破損しています。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="device-metadata-package-errors--0x500000xx-"></a>デバイス メタデータ パッケージのエラー (0x500000xx)  
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エラー コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>50000011</p></td>
<td align="left"><p><em>.Devicemetadata ms</em>キャビネット (<em>cab</em>) ファイルが破損しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>50000012</p></td>
<td align="left"><p><em>.Devicemetadata ms</em> cab ファイルには、正しいデバイス メタデータの構造はありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>50000021</p></td>
<td align="left"><p><em>PackageInfo.xml</em>がありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>50000022</p></td>
<td align="left"><p><em>PackageInfo.xml</em>形式が正しくありませんし、解析できません。</p>
<div class="alert">
<strong>注</strong>このエラー コードには、ケースが含まれています場所か、 <em>PackageInfo.xml</em>ドキュメントには、必要な要素がありません。 または、1 つ以上の要素の無効な構文に基づく、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff549614" data-raw-source="[PackageInfo XML Schema](https://msdn.microsoft.com/library/windows/hardware/ff549614)">PackageInfo XML。スキーマ</a>します。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td align="left"><p>50000031</p></td>
<td align="left"><p><em>DeviceInfo.xml</em>がありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>50000032</p></td>
<td align="left"><p><em>DeviceInfo.xml</em>形式が正しくありませんし、解析できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>50000033</p></td>
<td align="left"><p><em>DeviceInfo.xml</em>必須の要素がありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>50000034</p></td>
<td align="left"><p>内の要素<em>DeviceInfo.xml</em>無効な XML スキーマ定義に基づいています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>50000041</p></td>
<td align="left"><p><em>WindowsInfo.xml</em>がありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>50000042</p></td>
<td align="left"><p><em>WindowsInfo.xml</em>形式が正しくありませんし、解析できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>50000043</p></td>
<td align="left"><p><em>WindowsInfo.xml</em>必須の要素がありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>50000044</p></td>
<td align="left"><p>内の要素<em>WindowsInfo.xml</em>無効な XML スキーマ定義に基づいています。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="wmis-query--0x7000xxxx-"></a>WMIS クエリ (0x7000xxxx)  
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エラー コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>70000408</p></td>
<td align="left"><p>WMIS サーバーがダウンではありませんが、要求がタイムアウトしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>70000500</p></td>
<td align="left"><p>WMIS サーバーには、内部エラーが返されますが、詳細なエラー コードが使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>70000503</p></td>
<td align="left"><p>WMIS サーバーがビジー状態と、要求を処理することはできません。</p></td>
</tr>
</tbody>
</table>

 

 

 





