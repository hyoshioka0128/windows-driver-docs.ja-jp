---
ms.assetid: bb73768e-0ac9-4377-9caa-c0cce1d10bb8
title: ドライバーのテスト
description: ドライバーのテスト
ms.date: 06/28/2018
ms.localizationpriority: medium
ms.openlocfilehash: 53fa185c23d5d2b7c3f99e74d27482ff065f4d2c
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "67427688"
---
# <a name="testing-a-driver"></a>ドライバーのテスト

WDK は Visual Studio にドライバー テスト インターフェイスを追加して、ネットワーク上のリモート テスト コンピューターでドライバーのビルド、展開、インストール、テストを実行できるようにします。 WDK にはデバイス ドライバー テストのコレクションも用意されていて、ドライバーの機能のテストに使うことができます。 Visual Studio のドライバー テスト テンプレートを使って、テストをカスタマイズしたり、独自のドライバー テストを作ることもできます。

## <a name="span-idvideo_demonstrationspanspan-idvideo_demonstrationspanspan-idvideo_demonstrationspanvideo-demonstration"></a><span id="Video_Demonstration"></span><span id="video_demonstration"></span><span id="VIDEO_DEMONSTRATION"></span>ビデオ デモンストレーション


このビデオでは、テスト グループでドライバー関連のテストを実行する方法について説明します。

<iframe class="video-iframe" style="width: 100%; height: 550px;" frameborder="0" allowfullscreen="true" src ="https://www.microsoft.com/videoplayer/embed/e12e5ce5-b41f-4b91-ab5f-69598ccdcb57?autoplay=false"></iframe> 

ここでは、ドライバーのテストに関するいくつかの戦略と、テスト用に使うリモート コンピューターの選択および構成方法に関する情報について説明します。

ドライバーの一般配布の準備をするには、[Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893) を実行する必要があります。 Windows 認定プログラムと HCK の取得方法について詳しくは、「[Windows ハードウェア認定キット ユーザー ガイド](https://go.microsoft.com/fwlink/p/?linkid=227016)」をご覧ください。

WDK は、テスト バイナリと、コマンド ラインから Device Fundamental テストを簡単に実行できるようにするツールを提供します。
詳細については、[コマンド ラインでの DevFund テストの実行に関するページ](https://review.docs.microsoft.com/windows-hardware/drivers/devtest/run-devfund-tests-via-the-command-line)を参照してください。

## 
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
<td align="left"><p><a href="strategies-for-testing-drivers-during-development.md" data-raw-source="[Tips for testing drivers during development](strategies-for-testing-drivers-during-development.md)">開発中のドライバーのテストに関するヒント</a></p></td>
<td align="left"><p><strong>テストを開始するタイミング。</strong> ドライバーの要件がある場合はすぐに、テスト ケースの設計を開始して、重要な要件が実装されていることをテストできます。 これまでの調査から、コード内に欠陥が存在する時間が長ければ長いほど、コード内の欠陥の発見と修正にかかるコストは大きくなります。 開発サイクルの初期段階で欠陥を発見して修正できれば、コードがリリースおよび配布された後に欠陥を発見した場合に比べて、かかるコストも被害も小さくてすみます。 テスト ケースを早めに作成することは、設計上の問題の発見にも役立ちます。</p>
<p></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="testing-a-driver-at-runtime.md" data-raw-source="[How to test a driver at runtime using Visual Studio](testing-a-driver-at-runtime.md)">Visual Studio を使って実行時にドライバーをテストする方法</a></p></td>
<td align="left"><p>WDK 拡張機能は Visual Studio にドライバー テスト インターフェイスを提供して、ネットワーク上のテスト コンピューターで簡単にドライバーのビルド、展開、インストール、テストを実行できるようにします。 WDK にはデバイス ドライバー テストのコレクションが用意されていて、ドライバーの機能のテストに使うことができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="how-to-write-a-driver-test-.md" data-raw-source="[How to write a driver test using a Driver Test template](how-to-write-a-driver-test-.md)">ドライバー テスト テンプレートを使ってドライバー テストを作成する方法</a></p></td>
<td align="left"><p>Windows Driver Kit (WDK) for Windows 8 を使って、独自のドライバー テストを作成したり、提供されているテストの一部をカスタマイズすることができます。 Microsoft Visual Studio Ultimate 2012 用に WDK で提供されているドライバー テスト フレームワークを使って、作成したテストをリモート テスト コンピューターに展開できます。</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>参照

[ドライバーの検証用ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-verifying-drivers)

 





