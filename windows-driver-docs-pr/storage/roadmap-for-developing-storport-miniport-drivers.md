---
title: Storport ミニポート ドライバーの開発のロードマップ
description: Storport ミニポート ドライバーの開発のロードマップ
ms.assetid: 43a8f1ee-b2d3-4f97-b7e5-d59790ca6754
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae8919adecfd8ec523acb47acf5a0b6c151b74d4
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606548"
---
# <a name="roadmap-for-developing-storport-miniport-drivers"></a>Storport ミニポート ドライバーの開発のロードマップ

![幹線道路に "wdk" というテキストがあるロードマップの図](images/wdkroadmap-th.png)Storport ミニポートドライバーを作成するには、次の手順を実行します。

1. **Windows のアーキテクチャとドライバーについて説明します。**

    Windows でのドライバーの動作の基本を理解しておくことが重要です。 基本を理解することで、適切な設計上の決定を行い、開発プロセスを効率化することができます。 [すべてのドライバー開発者向けの概念を](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)ご覧ください。

2. **Storport ミニポートドライバーの基礎について説明します。**

    Storport ミニポートドライバーの基礎については、 [Windows Storage ドライバーのアーキテクチャ](storage-driver-architecture.md)、 [storport によって提供される機能](capabilities-provided-by-storport.md)、および storport[ミニポートドライバーを使用した storport のインターフェイスに関する](storport-s-interface-with-storport-miniport-drivers.md)ページを参照してください。

3. **追加の storport ミニポートドライバーの設計上の決定を決定します。**

   設計上の決定を行う方法については、「 [storport で提供される機能](capabilities-provided-by-storport.md)」、「[ストレージクラスドライバーを使用した storport のインターフェイス](storport-s-srb-interface-with-the-storage-class-driver.md)」、「[ストレージ仮想ミニポートドライバー](storage-virtual-miniport-drivers--when-are-they-appropriate-.md)」を[参照して](making-scsi-port-miniport-drivers-work-with-storport.md)ください。

4. **Windows Vista 以降のオペレーティングシステムでの storport ミニポートドライバーについて説明します。**

    Windows Driver Kit (WDK) の「 [Storport の履歴](history-of-storport.md)」を参照してください。

5. **Windows ドライバーのビルド、テスト、およびデバッグのプロセスとツールについて説明します。**

   ドライバーのビルドは、ユーザーモードアプリケーションのビルドと同じではありません。 Windows ドライバーのビルド、デバッグ、およびテストプロセス、ドライバー署名、および Windows ロゴテストに関する情報については、「[ドライバーの開発、テスト、および展開](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。 ツールのビルド、テスト、検証、およびデバッグについては、「[ドライバー開発ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/index)」を参照してください。

6. **Storport ミニポートドライバーのサンプルを確認します。**

    Storport ミニポートドライバーのサンプルにアクセスして確認するには、 [Windows Driver Kit (WDK) のサンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052)を参照してください。

7. **Storport ミニポートドライバーを開発、ビルド、テスト、およびデバッグします。**

    反復[的](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)なビルド、テスト、およびデバッグについては、「ドライバーのビルド」、「[ドライバーのテスト](https://docs.microsoft.com/windows-hardware/drivers)」、および「[ドライバーのデバッグ](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。 このプロセスを使用すると、動作するドライバーを確実にビルドできます。

8. **Storport ミニポートドライバーのドライバーパッケージを作成します。**

    詳細については、「[ドライバーパッケージの作成](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。

9. **Storport ミニポートドライバーに署名して配布します。**

    最後の手順では、ドライバーの署名と配布を行います (必要に応じて)。 ドライバーが Windows ハードウェア認定に対して定義されている品質基準を満たしている場合は、Microsoft Windows Update プログラムを通じて配布できます。 詳細については、「[ドライバーパッケージの配布](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。

基本的な手順は次のとおりです。 個々のドライバーのニーズに基づいて、追加の手順が必要になる場合があります。
