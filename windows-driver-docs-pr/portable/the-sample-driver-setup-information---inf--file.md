---
Description: サンプル ドライバー セットアップ情報 (.inf) ファイル
title: サンプル ドライバー セットアップ情報 (.inf) ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b24563cf737fa71dc3594efb68d8aa0f9825263a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375212"
---
# <a name="the-sample-driver-setup-information-inf-file"></a>サンプル ドライバー セットアップ情報 (.inf) ファイル


WpdHelloWorldDriver プロジェクトには、という名前のセットアップ情報 (.inf) ファイルが含まれています。 *WpdHelloWorldDriver.inf*します。 このファイルには、UMDF パラメーターと WUDF 共同インストーラーによって必要なディレクティブが含まれています。 ただし、このファイルは、パラメーターと WPD に排他的であるディレクティブも含みます。 次の表は、これら WPD に固有のパラメーター、ディレクティブ、およびセクションを示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">セクション</th>
<th align="left">ディレクティブまたはパラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Basic_Install.CoInstaller_AddReg</td>
<td align="left"></td>
<td align="left">このセクションが必要です。
<ul>
<li><em>WudfCoInstaller.dll</em>共同インストーラーとして表示する必要があります。</li>
<li>Reg のルートは、"HKR"である必要があります。</li>
<li>種類は 0x10000 である必要があります。</li>
<li>レジストリのディレクティブは、存在する必要があります。</li>
</ul>
<p>例: <code>[Basic_Install.CoInstallers_AddReg]</code></p>
<p><code>HKR,,CoInstallers32,0x00010000,"WUDFCoInstaller.dll"</code></p></td>
</tr>
 <tr class="even">
<td align="left">Basic_Install.wdf</td>
<td align="left">UmdfService ディレクティブ</td>
<td align="left">このディレクティブが必要です。
<ul>
<li>このディレクティブは、形式は。"UmdfService ServiceInstallSection、ServiceName ="。</li>
<li>参照先のセクション ("ServiceInstallSection") が存在する必要があります。</li>
<li>UmdfServiceOrder ディレクティブによって指定されたサービス名 ("ServiceName") を使用する必要があります。</li>
</ul>
<p>例: <code>[Basic_Install.Wdf]</code></p>
<p><code>UmdfService=WpdHelloWorldDriver, WpdHelloWorldDriver_Install</code></p>
<p><code>UmdfServiceOrder=WpdHelloWorldDriver</code></p></td>
</tr>
<tr class="odd">
<td align="left">DDInstall.Services</td>
<td align="left">ディレクティブが含まれています</td>
<td align="left">このディレクティブは、ドライバー、MTP クラス ドライバーのコンポーネントを再利用する場合に必要です。 それ以外の場合は表示されません。
<p>必要なシステム ファイルは、適切な包含を使用して参照する必要があります。 またはディレクティブを必要があります。 (これらのファイルは<em>WpdMtpDr.dll</em>、 <em>WpdMtp.dll</em>、 <em>WpdMtpUs.dll</em>、 <em>WpdConns.dll</em> (Windows Vista の場合) の場合、いずれかの<em>WpdUsb.sys</em> (Windows Vista) の場合、または<em>WinUsb.sys</em> (Windows 7 以降))。 必要なサービス ファイルを参照も必要があります。 (参照を必要とする 1 つのサービス ファイルが<em>WpdUsb.sys</em> (Windows Vista) の場合、または<em>WinUSB.sys</em> (Windows 7 以降).)</p></td>
</tr>
<tr class="even">
<td align="left">DDInstall.Services</td>
<td align="left">ディレクティブを必要があります。</td>
<td align="left">このディレクティブは、ドライバー、MTP クラス ドライバーのコンポーネントを再利用する場合に必要です。 それ以外の場合は表示されません。
<p>必要なシステム ファイルは、適切な包含を使用して参照する必要があります。 またはディレクティブを必要があります。 (これらのファイルは。<em>WpdMtpDr.dll</em>、 <em>WpdMtp.dll,WpdMtpUs.dll</em>、 <em>WpdConns.dll</em> (Windows Vista の場合) の場合、どちらか<em>WpdUsb.sys</em> (for Windows Vista の場合) または<em>WinUsb.sys</em> (Windows 7 以降))。 必要なサービス ファイルを参照も必要があります。 (参照を必要とする 1 つのサービス ファイルが<em>WpdUsb.sys</em> (Windows Vista) の場合、または<em>WinUSB.sys</em> (Windows 7 以降).)</p></td>
</tr>
<tr class="odd">
<td align="left">Device_AddReg</td>
<td align="left">EnableDefaultAutoPlaySupport ディレクティブ</td>
<td align="left">このディレクティブが必要です。
<ul>
<li>Reg のルートは、"HKR"である必要があります。</li>
<li>種類は 0x10001 である必要があります。</li>
<li>有効な値 (0 または 1) を設定する必要があります。</li>
</ul>
<p>以下に例を示します。</p>
<p><code>[Device_AddReg]</code></p>
<p><code>HKR,,"EnableDefaultAutoPlaySupport",0x10001,1</code></p></td>
</tr>
<tr class="even">
<td align="left">Device_AddReg</td>
<td align="left">EnableLegacySupport ディレクティブ</td>
<td align="left">このディレクティブが必要です。
<ul>
<li>Reg のルートは、"HKR"である必要があります。</li>
<li>種類は 0x10001 である必要があります。</li>
<li>有効な値 (0、1、2、または 3) を設定する必要があります。</li>
</ul>
<p>以下に例を示します。</p>
<p><code>[Device_AddReg]</code></p>
<p><code>HKR,,"EnableLegacySupport",0x10001,1</code></p></td>
</tr>
<tr class="odd">
<td align="left">Device_AddReg</td>
<td align="left">UseWiaAutoPlay ディレクティブ</td>
<td align="left">このディレクティブは省略可能です。
<ul>
<li>Reg のルートは、"HKR"である必要があります。</li>
<li>種類は 0x10001 である必要があります。</li>
<li>有効な値 (0 または 1) を設定する必要があります。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left">インストール</td>
<td align="left">UmdfLibraryVersion ディレクティブ</td>
<td align="left">このディレクティブが必要です。
<p>このディレクティブは、の形式にする必要があります: n.n.n</p>
<p>例: <code>[WpdHelloWorldDriver_Install]</code></p>
<p><code>UmdfLibraryVersion=1.0.0</code></p></td>
</tr>
<tr class="odd">
<td align="left">ServiceInstall</td>
<td align="left">ErrorControl ディレクティブ</td>
<td align="left">このディレクティブが必要です。
<p>このディレクティブは、1 の値を指定する必要があります。</p>
<p>例: <code>[WUDFRD_ServiceInstall]</code></p>
<p><code>ErrorControl=1</code></p></td>
</tr>
<tr class="even">
<td align="left">ServiceInstall</td>
<td align="left">ServiceType ディレクティブ</td>
<td align="left">このディレクティブが必要です。
<p>このディレクティブは、1 の値を指定する必要があります。</p>
<p>以下に例を示します。</p>
<p><code>[WUDFRD_ServiceInstall]</code></p>
<p><code>ServiceType=1</code></p></td>
</tr>
<tr class="odd">
<td align="left">ServiceInstall</td>
<td align="left">StartType ディレクティブ</td>
<td align="left">このディレクティブが必要です。
<p>このディレクティブは、3 の値を指定する必要があります。</p>
<p>以下に例を示します。</p>
<p><code>[WUDFRD_ServiceInstall]</code></p>
<p><code>StartType=3</code></p></td>
</tr>
<tr class="even">
<td align="left">バージョン</td>
<td align="left">クラスのパラメーター</td>
<td align="left">このパラメーターは必須です。 "WPD"に設定する必要があります。
<p>以下に例を示します。</p>
<pre space="preserve"><code>[Version]
Class=WPD</code></pre></td>
</tr>
<tr class="odd">
<td align="left">バージョン</td>
<td align="left">ClassGuid パラメーター</td>
<td align="left">このパラメーターは必須です。 有効な GUID に設定する必要があります。
<p>以下に例を示します。</p>
<pre space="preserve"><code>[Version]
ClassGuid={EEC5AD98-8080-425f-922A-DABF3DE3F69A}</code></pre></td>
</tr>
<tr class="even">
<td align="left">WpdHelloWorldDriver_Install</td>
<td align="left">DriverCLSID ディレクティブ</td>
<td align="left">このディレクティブが必要です。
<p>このディレクティブは、適切な形式の GUID を指定する必要があります。</p>
<p>以下に例を示します。</p>
<pre space="preserve"><code>[WpdHelloWorldDriver_Install]
DriverCLSID="{EC7445EE-BC00-4CED-AFE7-A52849F10239}"</code></pre></td>
</tr>
<tr class="odd">
<td align="left">WpdHelloWorldDriver_Install</td>
<td align="left">ServiceBinary ディレクティブ</td>
<td align="left">このディレクティブが必要です。
<p>このディレクティブは、フォームのパスを指定する必要があります"% 12%\wudfrd.sys"。</p>
<p>以下に例を示します。</p>
<p><code>[WUDFRD_ServiceInstall]</code></p>
<p><code>ServiceBinary=%12%\WUDFRd.sys</code></p></td>
</tr>
</tbody>
</table>

 

 

 




