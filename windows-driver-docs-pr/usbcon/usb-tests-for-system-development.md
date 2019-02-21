---
Description: If you are building a new system, the tests in this topic are recommended.
title: システムの開発用の USB テストをお勧めします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b234a7c1d38095a8eccc24a13c78da4085d5bfe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536065"
---
# <a name="recommended-usb-tests-for-system-development"></a>システムの開発用の USB テストをお勧めします。


新しいシステムを構築する場合、このトピックのテストがお勧めします。

このトピックに記載の DF テストを実行するが必要[MUTT デバイス](microsoft-usb-test-tool--mutt--devices.md)します。 ステージによっては、このコマンドを実行して、デバイスのドライバーを更新する必要があります。

`muttutil -updatedriver <driver_inf>.inf`

[MuttUtil](muttutil.md)にツールが含まれ、 [MUTT ソフトウェア パッケージ](mutt-software-package.md)します。

新しいシステムを構築する場合、推奨される USB HCK テストを示します。

## <a name="stage-1system-bring-up"></a>第 1 段階: システム bring アップ


-   [DF – (Basic) の前後に IO とスリープ](https://msdn.microsoft.com/library/windows/hardware/dn247481.aspx)
-   [DF - PNP (無効にする に、有効にする) (Basic) の前後に IO の前に](https://msdn.microsoft.com/library/windows/hardware/dn260411.aspx)
-   [USB Exposed ポート コント ローラーのテスト](https://msdn.microsoft.com/library/windows/hardware/hh998021.aspx)
-   [USB xHCI Transfer Speed Test](https://msdn.microsoft.com/library/windows/hardware/hh997864.aspx)
-   [USB3 終了](https://msdn.microsoft.com/library/windows/hardware/jj124672.aspx)

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>システムの xHCI コント ローラーにそれぞれ、このトポロジを構成します。</th>
<th>推奨されるテストの実行</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ol>
<li>システムの SuperSpeed ポートに USB 3.0 ハブを接続します。</li>
<li><p>USB 3.0 ハブのダウン ストリーム SuperMUTT を接続します。</p>
<p></p>
<p><strong>デバイス ドライバー:  </strong>SuperMUTT をデバイスのデバイス ドライバーとして Winusb.sys 必要があります。 次のコマンドを実行します。</p>
<p><code>muttutil -updatedriver usbfx2.inf</code></p>
<p><img src="images/xhci-superspeedhub-supermutt.png" alt="System bring-up topology" /></p></li>
</ol>
<div class="alert">
<strong>注</strong>  タイプ A コネクタがないかどうかは、アダプターがシステムに付属する必要があります。
</div>
<div>
 
</div></td>
<td><ol>
<li>Windows HCK Studio での<strong>選択</strong>] タブで [<strong>デバイス マネージャー</strong>します。</li>
<li>XHCI コント ローラーとそのルート ハブを選択します。
<div class="alert">
<strong>注</strong>  コント ローラーをすばやく見つけるには、入力&quot;xhci&quot;で検索します。
</div>
<div>
 
</div></li>
<li><strong>ビューによって</strong>一覧で、選択<strong>基本的な</strong>します。</li>
<li>推奨される、選択したコント ローラーを実行します。</li>
</ol></td>
</tr>
</tbody>
</table>

 

## <a name="stage-2system-integration"></a>ステージ 2-システムとの統合


-   [DF - 再起動の再起動と IO (機能) の前後](https://msdn.microsoft.com/library/windows/hardware/dn260266.aspx)
-   [DF - スリープと PNP (無効および有効にする) (機能) の前後に IO の前に](https://msdn.microsoft.com/library/windows/hardware/dn260391.aspx)
-   [USB xHCI Transfer Speed Test](https://msdn.microsoft.com/library/windows/hardware/hh997864.aspx)

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>システムの xHCI コント ローラーにそれぞれ、このトポロジを構成します。</th>
<th>推奨されるテストの実行</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p>
<p>システムの xHCI コント ローラーにそれぞれ、このトポロジを構成します。</p>
<ol>
<li>システムの SuperSpeed ポートに USB 3.0 ハブを接続します。</li>
<li><p>USB 3.0 ハブのダウン ストリーム SuperMUTT を接続します。</p>
<p><strong>デバイス ドライバー:  </strong>SuperMUTT をデバイスのデバイス ドライバーとして Usbtcd.sys 必要があります。 次のコマンドを実行します。</p>
<p><code>muttutil -updatedriver usbtcd.inf</code></p></li>
<li>USB 3.0 ハブのダウン ストリーム SuperMUTT パックに接続します。</li>
</ol>
<p><img src="images/xhci-system-integration.png" alt="System integration topology" /></p>
<p></p>
<div class="alert">
<strong>注</strong>  タイプ A コネクタがないかどうかは、アダプターがシステムに付属する必要があります。
</div>
<div>
 
</div></td>
<td><p>テストを実行します。</p>
<ol>
<li><strong>選択</strong>] タブで [<strong>デバイス マネージャー</strong>します。</li>
<li>XHCI コント ローラーとそのルート ハブを選択します。
<div class="alert">
<strong>注</strong>  コント ローラーをすばやく見つけるには、入力&quot;xhci&quot;で検索します。
</div>
<div>
 
</div></li>
<li><strong>ビューによって</strong>一覧で、選択<strong>機能</strong>します。</li>
<li>推奨される、選択したコント ローラーを実行します。</li>
</ol></td>
</tr>
</tbody>
</table>

 

## <a name="stage-3system-tuneup"></a>第 3 段階: システムのチューン アップ


システム 1

-   [DF - (認定) 中に IO とスリープ](https://msdn.microsoft.com/library/windows/hardware/dn247416.aspx)
-   [DF - 同時実行ハードウェアおよびオペレーティング システム (CHAOS) テスト (認定)](https://msdn.microsoft.com/library/windows/hardware/hh998603.aspx)

システム 2

-   [DF - スリープと PNP (無効および有効にする) (機能) の前後に IO の前に](https://msdn.microsoft.com/library/windows/hardware/dn260391.aspx)
-   [USB xHCI Transfer Speed Test](https://msdn.microsoft.com/library/windows/hardware/hh997864.aspx)

システム (ドッキング ステーションがサポートされている) 場合 3

-   テストを実行、[システム インテグレーションのステージ](#stage2)ドッキングされているシステム。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>システムの xHCI コント ローラーにそれぞれ、このトポロジを構成します。</th>
<th>推奨されるテストの実行</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>システム 1</p>
<p>参照してください<a href="#stage1" data-raw-source="[system bring-up topology](#stage1)">システム bring アップ トポロジ</a>します。</p>
<p><strong>デバイス ドライバー:  </strong>SuperMUTT をデバイスのデバイス ドライバーとして Usbtcd.sys 必要があります。 次のコマンドを実行します。</p>
<p><code>muttutil -updatedriver usbtcd.inf</code></p>
<p>システム 2</p>
<p>システムの xHCI コント ローラーにそれぞれ、このトポロジを構成します。</p>
<ol>
<li>システムの SuperSpeed ポートに USB 3.0 ハブを接続します。</li>
<li>USB 3.0 ハブのダウン ストリーム SuperMUTT を接続します。</li>
<li>USB 3.0 ハブのダウン ストリーム SuperMUTT パックに接続します。</li>
<li>USB 3.0 ハブのダウン ストリーム MUTT パックに接続します。</li>
<li>最初のハブで、ダウン ストリーム SuperMUTT パックでは、4 つ自己供給 USB 3.0 ハブ ダウン ストリーム (チェーンを形成する) 他を接続します。</li>
<li>接続、MUTT (または SuperMUTT パック) チェーン内の最後の USB 3.0 ハブのダウン ストリーム。</li>
</ol>
<img src="images/xhci-superspeedhub-hub-daisy.png" alt="System tuning topology" />
<p>システム (ドッキング ステーションがサポートされている) 場合 3</p>
<p>参照してください<a href="#stage2" data-raw-source="[system integration stage](#stage2)">システム インテグレーションのステージ</a>します。</p></td>
<td><p>システム 1</p>
<ol>
<li><strong>選択</strong>] タブで [<strong>デバイス マネージャー</strong>します。</li>
<li>XHCI コント ローラーとそのルート ハブを選択します。
<div class="alert">
<strong>注</strong>  コント ローラーをすばやく見つけるには、入力&quot;xhci&quot;で検索します。
</div>
<div>
 
</div></li>
<li><strong>ビューによって</strong>一覧で、選択<strong>証明</strong>します。</li>
<li>推奨される、選択したコント ローラーを実行します。</li>
</ol>
<p>システム 2</p>
<ol>
<li><strong>選択</strong>] タブで [<strong>デバイス マネージャー</strong>します。</li>
<li>一覧に表示トポロジでは、すべての MUTT デバイスを選択します。
<div class="alert">
<strong>注</strong>  コント ローラーをすばやく見つけるには、入力&quot;MUTT&quot;で検索します。
</div>
<div>
 
</div></li>
<li><strong>ビューによって</strong>一覧で、選択<strong>機能</strong>します。</li>
<li>2 のシステムについて推奨されるテストを実行します。</li>
<li>システムにハブを接続するのにには、2 つのメーター長いケーブルを使用します。</li>
</ol>
<p>システム 3</p>
<ul>
<li><p>同じ<a href="#stage2" data-raw-source="[system integration topology](#stage2)">システム統合トポロジ</a>します。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[USB の Windows ハードウェア ラボ キット テスト](windows-hardware-certification-kit-tests-for-usb.md)  



