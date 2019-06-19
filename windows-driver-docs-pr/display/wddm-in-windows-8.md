---
title: WDDM 1.2 と Windows 8
description: このセクションでは、Windows 8 以降で使用可能なある新機能と拡張 Windows Display Driver Model (WDDM) バージョン 1.2 の詳細を説明します。 ハードウェア要件、実装のガイドラインと使用シナリオについても説明します。
ms.assetid: 8757ADDD-EDCA-4C09-BB71-2ED925DB2E41
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46a5481b6875026429565aaa1dd9066a2b013046
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161548"
---
# <a name="wddm-12-and-windows-8"></a>WDDM 1.2 と Windows 8


このセクションでは、Windows 8 以降で使用可能なある新機能と拡張 Windows Display Driver Model (WDDM) バージョン 1.2 の詳細を説明します。 ハードウェア要件、実装のガイドラインと使用シナリオについても説明します。

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
<td align="left"><p><a href="wddm-v1-2-features.md" data-raw-source="[WDDM 1.2 features](wddm-v1-2-features.md)">WDDM 1.2 機能</a></p></td>
<td align="left"><p>このトピックでは、パフォーマンス、信頼性、および全体的なエンド ユーザー エクスペリエンスを向上させる新しい拡張機能がいくつか含まれている WDDM バージョン 1.2 の機能セットを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="advances-to-the-display-infrastructure.md" data-raw-source="[Advances to the display Infrastructure](advances-to-the-display-infrastructure.md)">インフラストラクチャの画面に進みます</a></p></td>
<td align="left"><p>Windows 8 の強化し、ユーザー エクスペリエンスを向上するため、表示のインフラストラクチャをさらに最適化します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="direct3d-features-and-requirements.md" data-raw-source="[Direct3D features and requirements in WDDM 1.2](direct3d-features-and-requirements.md)">Direct3D の機能および WDDM 1.2 での要件</a></p></td>
<td align="left"><p>マイクロソフトの Direct3D には、3-D グラフィックス、複雑な視覚化とゲーム開発ソフトウェア アプリケーションで広く使用されている Api の豊富なコレクションが用意されています。 このセクションでは、機能の改善と Windows 8 の Direct3D ソフトウェアおよびハードウェア要件について説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="graphics-inf-requirements.md" data-raw-source="[Graphics INF requirements in WDDM 1.2](graphics-inf-requirements.md)">WDDM 1.2 でグラフィックス INF 要件</a></p></td>
<td align="left"><p>Windows 8 版の WDDM ドライバーでは、グラフィックス ドライバーの INF 変更が必要です。 最も注目すべき変更は、特徴のスコアです。 WDDM 1.2 ドライバーには、WDDM ドライバーを以前よりも高い特徴のスコアが必要です。 このセクションには、Windows 8 のグラフィック ドライバーのすべての関連する INF 要件がについて説明します</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="installation-scenarios.md" data-raw-source="[WDDM 1.2 installation scenarios](installation-scenarios.md)">WDDM 1.2 のインストール シナリオ</a></p></td>
<td align="left"><p>Windows 8 のインストールのグラフィックス ドライバーの動作は、可能であれば、お客様がテストされ、Windows 8 認定のグラフィック ドライバーを取得、設計されています。 この動作は、このセクションで説明されている規則によって定義されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wddm-v1-2-driver-enforcement-guidelines.md" data-raw-source="[WDDM 1.2 driver enforcement guidelines](wddm-v1-2-driver-enforcement-guidelines.md)">WDDM 1.2 ドライバーの適用ガイドライン</a></p></td>
<td align="left"><p>このセクションでは、WDDM 1.2 ドライバーの適用ガイドラインについて説明します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idintroductionspanspan-idintroductionspanspan-idintroductionspanintroduction"></a><span id="Introduction"></span><span id="introduction"></span><span id="INTRODUCTION"></span>概要


WDDM は Windows XP の代わりに Windows Vista で導入されたまたは[Windows 2000 Display Driver Model (XDDM)](windows-2000-display-driver-model-design-guide.md)します。 Windows Vista に導入されて以来、WDDM アーキテクチャがデスクトップ コンポジションなどの新機能を有効にする機能を提供する、フォールト トレランス、ビデオ メモリ マネージャー、GPU のスケジューラを強化、Direct3D サーフェスのプロセスの共有をクロスとします。 WDDM は、マイクロソフトの Direct3D 9 ピクセル シェーダー 2.0 以上でがあった WDDM 機能をサポートするために必要なハードウェア機能をすべて最新のグラフィックス デバイス用に設計されています。 Windows Vista の WDDM が"WDDM 1.0"として参照

Windows 7 の Windows 7 の機能と機能をサポートするため、ドライバー モデルに増分の変更を加えてし、"WDDM 1.1"と呼ばれていました WDDM 1.1 は、WDDM 1.0 の厳密なスーパー セットです。 WDDM 1.1 には、Microsoft direct3d11 では、サポートが導入されました。 Windows グラフィックス デバイス インターフェイス (GDI) ハードウェア アクセラレーションにより、接続と構成が表示されたら、DirectX ビデオ アクセラレータ (VA) 高精細 (DXVA HD)、およびその他の多くの機能です。 これらの機能の詳細については、次を参照してください。、 [Windows 7 用グラフィックス ガイド](https://go.microsoft.com/fwlink/p/?linkid=327733)します。

Windows 8 には、配列の新機能とグラフィックス ドライバーの変更を必要とする機能が導入されています。 増分変更は、エンドユーザーと開発者のメリットし、システムの信頼性を向上させます。 これらの Windows 8 の機能を有効にする WDDM ドライバー モデルは"WDDM 1.2"と呼ばれます WDDM 1.2 では、WDDM 1.1 および WDDM 1.0 のスーパー セットです。 これらの変更は、この表に示すように、簡単な形式で表現できます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オペレーティング システム</th>
<th align="left">サポートされているドライバー モデル</th>
<th align="left">サポートされている Direct3D のバージョン</th>
<th align="left">有効になっている機能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Windows Vista</td>
<td align="left">WDDM 1.0
<p>サーバーで制限付きの UMPC XDDM</p></td>
<td align="left">D3D9、D3D10</td>
<td align="left">スケジュール設定、メモリ管理、フォールト トレランス、D3D9 & 10</td>
</tr>
<tr class="even">
<td align="left">Windows Vista SP1/Windows 7 クライアント パック</td>
<td align="left"><p>WDDM 1.05</p>
<p>Server 2008 で XDDM</p></td>
<td align="left">D3D9, D3D10, D3D10.1</td>
<td align="left">+ D3D10、D3D 10.1 で BGRA のサポート</td>
</tr>
<tr class="odd">
<td align="left">Windows 7</td>
<td align="left"><p>WDDM 1.1</p>
<p>Server 2008 R2 で XDDM</p></td>
<td align="left">D3D9、D3D10、D3D10.1、D3D11</td>
<td align="left">GDI のハードウェアの高速化 DXVA HD、D3D11</td>
</tr>
<tr class="even">
<td align="left">Windows 8</td>
<td align="left">WDDM 1.2</td>
<td align="left">D3D9、D3D10、D3D10.1、D3D11、D3D11.1</td>
<td align="left">D3D11.1、回転、ステレオスコ ピック 3d 表示、D3D11 ビデオを滑らかなど。</td>
</tr>
</tbody>
</table>

 

**注**   Windows 8 では、WDDM 1.2 XDDM はサポートされなくと XDDM ドライバーが Windows 8 クライアントまたはサーバーに読み込まれない。 従来、XDDM に依存するシナリオでは、Windows 8 は、次の表に示すように WDDM への移行をできます。

独立系ハードウェア ベンダー (Ihv) およびシステム ビルダは、顧客向けに最適な代替 WDDM ソリューションを採用する必要があります。 これは、Windows 8 システムが常にある WDDM ドライバーを意味します。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">現在使用しています。</th>
<th align="left">XDDM シナリオ WDDM をサポート</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">XDDM VGA ドライバー</td>
<td align="left">Microsoft 基本ディスプレイ ドライバー</td>
</tr>
<tr class="even">
<td align="left">XDDM IHV ドライバー</td>
<td align="left">システム ビルダーは、取得する IHV を使用する必要があります。
<ul>
<li>表示専用 WDDM ドライバーまたは</li>
<li>完全なグラフィックス WDDM ドライバー</li>
</ul>
<p>Microsoft Basic ディスプレイ ドライバーまたは</p></td>
</tr>
<tr class="odd">
<td align="left">XDDM 仮想化ドライバー</td>
<td align="left">システム ビルダーは、新しい Display-Only 仮想化ドライバーを入手する IHV を使用する必要があります。</td>
</tr>
<tr class="even">
<td align="left">Int10 の CSM の Unified Extensible Firmware Interface (UEFI) のサポートします。</td>
<td align="left">UEFI グラフィックス出力プロトコル (GOP) のために必要なサポート不要になった</td>
</tr>
<tr class="odd">
<td align="left">リモート デスクトップ アクセス/コラボレーション</td>
<td align="left">デスクトップの重複 API</td>
</tr>
<tr class="even">
<td align="left">リモート セッションのドライバー</td>
<td align="left">変更なしではサポートされていません&lt;32 bpp モード</td>
</tr>
</tbody>
</table>

 

**注**   Microsoft ドライバーを提供して WDDM に基づく基本的な表示を先ほどインボックス XDDM Standard VGA driver の置換は、基本的な表示機能とソフトウェア ベースの 2-d および 3-D レンダリングを提供します。

 

WDDM 1.2 には、新しい種類のグラフィックス ドライバーでは、以下に示すように、特定のシナリオを対象とするが導入されています。

-   **WDDM の完全なグラフィックス ドライバー:** これは、2-d および 3-D の操作をサポートするハードウェアが高速こと WDDM ドライバーの完全なバージョンです。 このドライバーは、処理、レンダリング、表示、およびビデオ機能の完全な機能です。 WDDM 1.0 および WDDM 1.1 は、完全なグラフィックス ドライバーです。 すべての Windows 8 クライアント システムの主要なブート デバイスとして完全なグラフィックスおよび WDDM 1.2 デバイスが必要です。
-   **WDDM ドライバーのみを表示する**:このドライバーは、WDDM 1.2 ドライバーとしてのみサポートされているし、により、Ihv 運転表示専用のデバイスである WDDM ベースのカーネル モード ドライバーを作成します。 Windows では、ソフトウェアのシミュレートされた GPU を使用して、2 D または 3-D レンダリングを処理します。 表示専用デバイスは、クライアント システム上のプライマリのグラフィックス デバイスとしては使用できません。
-   **WDDM ドライバーのみを表示する**:このドライバーは、WDDM 1.2 ドライバーとしてのみサポートされているし、により、Ihv レンダリング機能のみをサポートする WDDM ドライバーを作成します。 レンダリング専用デバイスは、クライアント システム上のプライマリのグラフィックス デバイスとしては使用できません。

このテーブルは、サポートされているドライバーのカテゴリとドライバー モデルをまとめたものです。

| ドライバー モデル/ドライバーのカテゴリ | 完全なグラフィック | のみを表示します。 | 表示のみ |
|------------------------------|---------------|--------------|-------------|
| WDDM 1.0 (Windows Vista)     | 〇           | X           | X          |
| WDDM 1.1 (Windows 7)         | 〇           | X           | X          |
| WDDM 1.2 (Windows 8)         | 〇           | 〇          | 〇         |

 

このテーブルには、新しいドライバーの種類のシナリオの使用状況について説明します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"></th>
<th align="left">クライアント</th>
<th align="left">Server</th>
<th align="left">仮想環境で実行しているクライアント</th>
<th align="left">仮想サーバー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">完全なグラフィック</td>
<td align="left">ブート デバイスとして必要です。</td>
<td align="left">省略可能</td>
<td align="left">省略可能</td>
<td align="left">省略可能</td>
</tr>
<tr class="even">
<td align="left">表示のみ</td>
<td align="left">使用不可</td>
<td align="left">省略可能</td>
<td align="left">省略可能</td>
<td align="left">省略可能</td>
</tr>
<tr class="odd">
<td align="left">レンダリング専用</td>
<td align="left">プライマリ以外のアダプターとして (省略可能)</td>
<td align="left">省略可能</td>
<td align="left">省略可能</td>
<td align="left">省略可能</td>
</tr>
<tr class="even">
<td align="left">ヘッドレス</td>
<td align="left">使用不可</td>
<td align="left">省略可能</td>
<td align="left">なし</td>
<td align="left">なし</td>
</tr>
</tbody>
</table>

 

WDDM 1.2 は、Windows 8 に同梱されているすべてのシステムに必要です。 WDDM 1.0 および WDDM 1.1 は、Windows 8 で動作を続けます。 ただし、最適なエクスペリエンスと Windows 8 固有の機能が WDDM 1.2 ドライバーでのみ有効です。

 

 





