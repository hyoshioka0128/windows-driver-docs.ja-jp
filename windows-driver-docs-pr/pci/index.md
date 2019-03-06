---
title: PCI ドライバー プログラミング ガイド
description: PCI ドライバー プログラミング ガイド
ms.assetid: 014f6243-6166-42e1-9f0f-1a438c77fd78
keywords:
  - PCI WDK バス
  - 'バス WDK, PCI'
  - Peripheral Component Interconnect WDK バス
  - PCI ローカル バス仕様 WDK
  - 構成領域 WDK PCI
  - デバイス固有の構成領域 WDK PCI
  - 構成領域情報の要求 WDK PCI
  - 電源管理 WDK PCI
  - 電源管理機能データのクエリ
  - ヘッダー WDK PCI
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# <a name="pci-driver-programming-guide"></a>PCI ドライバー プログラミング ガイド


## <a name="supported-pcie-features-in-windows"></a>Windows でサポートされている PCIe 機能


次の表は、さまざまなバージョンの Windows でサポートされている PCIe 機能をまとめたものです。 詳細については、[公式の PCIe の仕様](http://www.pcisig.com/specifications/pciexpress/review_zone/)の指定のセクションをご覧ください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>Windows の最小バージョン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>サイズ変更可能な BAR 機能</p>
<p>セクション 7.22 をご覧ください。</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>アトミックの操作</p>
<p>セクション 6.15 をご覧ください。</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="odd">
<td><p>FW 待機時間の最適化のための ACPI の追加</p>
<p><a href="https://go.microsoft.com/fwlink/p/?LinkId=787058" data-raw-source="[ACPI Additions for FW Latency Optimizations]( https://go.microsoft.com/fwlink/p/?LinkId=787058)">FW 待機時間の最適化のための ACPI の追加</a>に関するページをご覧ください。</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>ATS/PRI</p>
<ul>
<li><a href="https://go.microsoft.com/fwlink/p/?LinkId=787061" data-raw-source="[ATS specification](https://go.microsoft.com/fwlink/p/?LinkId=787061)">ATS の仕様</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?LinkId=787060" data-raw-source="[Errata for the PCI Express&#174; Base Specification Revision 3.1, Single Root I/O Virtualization and Sharing Revision 1.1, Address Translation and Sharing Revision 1.1, and M.2 Specification Revision 1.0](https://go.microsoft.com/fwlink/p/?LinkId=787060)">PCI Express® Base Specification Revision 3.1、Single Root I/O Virtualization and Sharing Revision 1.1、Address Translation and Sharing Revision 1.1、および M.2 Specification Revision 1.0 の正誤表</a></li>
</ul></td>
<td><p>Windows 10</p></td>
</tr><td><p>Optimized Buffer Flush/Fill (OBFF)</p>
<p>セクション 6.19 をご覧ください。</p></td>
<td><p>Windows 8</p>
<p>Windows Server 2012</p></td>
</tr>
<tr class="even">
<td><p>Latency Tolerance Reporting (LTR) 機能</p>
<p>セクション 7.25 をご覧ください。</p></td>
<td><p>Windows 8</p>
<p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td><p>Alternative Routing-ID Interpretation (ARI)</p>
<p>セクション 6.13 をご覧ください。</p></td>
<td><p>Windows 8</p>
<p>Windows Server 2012</p></td>
</tr>
<tr class="even">
<td><p>Message Signaled Interrupt (MSI/MSI-X) のサポート</p>
<p>セクション 6.1.4 をご覧ください。</p></td>
<td><p>Windows Vista</p>
<p>Windows Server 2008 R2</p></td>
</tr>
<tr class="odd">
<td><p>TLP Processing Hints (TPH)</p>
<p>セクション 6.17 をご覧ください。</p></td>
<td><p>Windows 8</p>
<p>Windows Server 2012</p></td>
</tr>
<tr class="even">
<td><p>シングル ルート I/O 仮想化 (SR-IOV)</p>
<p>「<a href="https://msdn.microsoft.com/library/windows/hardware/hh440235" data-raw-source="[Single Root I/O Virtualization (SR-IOV)](https://msdn.microsoft.com/library/windows/hardware/hh440235)">Single Root I/O Virtualization (SR-IOV) (シングル ルート I/O 仮想化 (SR-IOV))</a>」をご覧ください。</p></td>
<td><p>Windows 8</p>
<p>Windows Server 2012</p></td>
</tr>
</tbody>
</table>





## <a name="in-this-section"></a>このセクションの内容


-   [PCI 電源の管理とデバイス ドライバー](https://msdn.microsoft.com/library/windows/hardware/dn607302)
-   [PCI デバイス構成領域へのアクセス](https://msdn.microsoft.com/library/windows/hardware/ff536890)
-   [I/O リソース使用量の削減](https://msdn.microsoft.com/library/windows/hardware/ff537424)
-   [開始デバイス IRP でのリソースの順序](https://msdn.microsoft.com/library/windows/hardware/ff537445)
-   [PCI Express のグラフィックスに関する FAQ](https://msdn.microsoft.com/library/windows/hardware/dn653979)
-   [PCI のサンプル](https://msdn.microsoft.com/library/windows/hardware/hh450892)


## <a name="see-also"></a>参照
-   [公式の PCIe の仕様](http://www.pcisig.com/specifications/pciexpress/review_zone/)

 

 




