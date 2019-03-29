---
Description: MTP セットアップ情報 (.inf) ファイル
title: MTP セットアップ情報 (.inf) ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f76f42c17479d35ea63ae846708bbf3900f3d6f6
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349185"
---
# <a name="the-mtp-setup-information-inf-file"></a>MTP セットアップ情報 (.inf) ファイル


Microsoft では、メディア転送プロトコル (MTP) をサポートするクラスのドライバーのセットを提供します。 デバイスは、MTP をサポートする場合は、これらのドライバーのいずれかを使用できます。 Microsoft は、クラスのドライバーだけでなく、クラス ドライバーをインストールするセットアップ情報 (.inf) ファイルを提供します。 このファイルの名前は*WpdMtp.inf*します。

MTP デバイスに固有の要件がある場合は、作成する新しいセットアップ情報 (.inf) ファイルの元のバージョンに基づいている*WpdMtp.inf*します。 (変更することはできません*WpdMtp.inf*直接)。

次の表に、特定のニーズ ディレクティブ内にある*WpdMtp.inf*および可能性の変更を指定されたディレクティブによって識別されるセクションを行うことができます。

次の表に、エントリには、次の 3 つのトランスポート (USB、IP、または Bluetooth) のいずれかをサポートできます。 各トランスポートが一意のインストール セクションが必要なことに注意します。 また Bluetooth トランスポートが Windows 7 でのみサポートされていることに注意します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ディレクティブを必要があります。</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">WPD を = 必要があります。MTP、WINUSB します。NT</td>
<td align="left">WPD します。MTP セクションでは、ドライバー ファイルがコピーされ、登録を識別します。 次は Windows Vista および Windows Media Player 11 に適用されます。
<pre space="preserve"><code>;;[DDInstall]
;;Include = wpdmtp.inf
;;Needs = WPD.MTP</code></pre>
<p>Windows 7 以降、 <em>WinUsb.sys</em>置き換えます<em>WpdUsb.sys</em> USB を使用して、コンピューターに接続するための MTP デバイスの下位のフィルター ドライバーとして。 次のディレクティブは、ベンダーの INF に含めるに必要な<em>WinUsb.inf</em>と特定の WinUSB セクション。</p>
<pre space="preserve"><code>;;[DDInstall]
;;Include = wpdmtp.inf, WINUSB.INF
;;Needs = WPD.MTP, WINUSB.NT</code></pre></td>
</tr>
<tr class="even">
<td align="left">WPD を = 必要があります。MTP します。登録</td>
<td align="left">WPD します。MTP します。登録のセクションでは、4 つのタスクを実現します。
<ol>
<li>カーネル モード ドライバーを登録します (など<em>WPDUSB.sys</em> Windows Vista または Windows XP でデバイスをインストールする場合は、下位のフィルター ドライバーとして)。</li>
<li>既定の MTP 自動再生のサポートを有効にします。</li>
<li>レガシ アプリケーションの互換性サポートを有効 (既定値 0 xffffffff は、デバイスの機能を照会する WPD クラスのインストーラーを使用)。</li>
<li>トランスポート ドライバーのクラス id を設定します。</li>
</ol>
<pre space="preserve"><code>;;[DDInstall.hw]
;;Include = wpdmtp.inf
;;Needs = WPD.MTP.Registration</code></pre></td>
</tr>
<tr class="odd">
<td align="left">Needs = WPD.MTP.Registration.Basic</td>
<td align="left">WPD します。MTP します。Registration.Basic セクションでは、タスク 2 および 3 に、前のリストをカスタマイズできます。 たとえば、0x02 の値を使用して 0x01 の値を使用して Windows Image Acquisition (WIA) または Windows メディア デバイス マネージャー (WMDM) をサポートするために、アプリケーションの互換性を設定することができます。
<pre space="preserve"><code>;;[DDInstall.hw]
;;Include = wpdmtp.inf
;;Needs = WPD.MTP.Registration.Basic</code></pre></td>
</tr>
<tr class="even">
<td align="left">WPD を = 必要があります。MTP します。サービス</td>
<td align="left">WPD します。MTP します。サービスでは、ドライバー サービス (および既定のサービス パラメーター) を追加します。 WUDF が含まれますと<em>WPDUSB.sys</em> (用、Windows Vista および Windows XP の場合のみ)。
<pre space="preserve"><code>;;[DDInstall.Services]
;;Include = wpdmtp.inf
;;Needs = WPD.MTP.Services</code></pre></td>
</tr>
<tr class="odd">
<td align="left">Needs = WPD.MTP.CoInstallers</td>
<td align="left">WPD します。MTP します。共同インストーラーのセクションでは、共同インストーラーを識別します。 (MTP デバイスをインストールするには Windows ユーザー モード ドライバー フレームワーク (UMDF) 共同インストーラーが使用されます。)
<p>このセクションでは、Windows 7、Windows Vista、および Windows Media Player 11 必要があります。 (そのでした、MTP ドライバー Windows Media Player 10 をサポートするために必要です。)</p>
<pre space="preserve"><code>;;[DDInstall.CoInstallers]
;;Include = wpdmtp.inf
;;Needs = WPD.MTP.CoInstallers</code></pre></td>
</tr>
<tr class="even">
<td align="left">必要な WPD.MTP.Wdf を =</td>
<td align="left">Windows ユーザー モード ドライバー フレームワーク (UMDF) サービスとそのバイナリ WPD.MTP.Wdf セクションを識別します (<em>WPDMTPDR.dll</em>)。
<p>このセクションでは、Windows 7、Windows Vista、および Windows Media Player 11 必要があります。 (そのでした、MTP ドライバー Windows Media Player 10 をサポートするために必要です。)</p>
<pre space="preserve"><code>;;[DDInstall.CoInstallers]
;;Include = wpdmtp.inf
;;Needs = WPD.MTP.Wdf</code></pre></td>
</tr>
</tbody>
</table>

 

 

 




