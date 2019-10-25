---
title: ドライバーのテストとデバッグ用のブート オプション変更ツール
description: ドライバーのテストとデバッグ用のブート オプション変更ツール
ms.assetid: 4fd58868-7a43-42e3-adf9-5a82593c1675
keywords:
- ツール WDK、ブートオプション
- ドライバー開発ツール WDK, ブートオプション
- ブートオプション WDK
- WDK ブートオプションのドライバーテスト
- ドライバーのテスト WDK ブートオプション
- デバッグドライバーの WDK ブートオプション
- ドライバーのデバッグ WDK ブートオプション
- オペレーティングシステムのブートオプション WDK
- 負荷構成の WDK ブートオプション
ms.date: 04/19/2019
ms.localizationpriority: medium
ms.openlocfilehash: ea275914a28b606b5e58bacf250db537108829f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840301"
---
# <a name="tools-for-changing-boot-options-for-driver-testing-and-debugging"></a>ドライバーのテストとデバッグ用のブート オプション変更ツール

Microsoft Windows オペレーティングシステムでドライバーをテストおよびデバッグするには、オペレーティングシステムの読み込み時に確立される機能を有効にして構成する必要があります。 これらの機能の設定は、ブートローダーがオペレーティングシステムやその他の起動可能なプログラムとデバイスをどのように読み込んで構成するかを決定する値として、*ブートオプション*に含まれています。


このセクションでは、ブートオプションを追加、削除、変更して、オペレーティングシステムの新しい負荷構成を作成する方法、およびブートエントリパラメーターを使用してドライバーのテストとデバッグの負荷構成をカスタマイズする方法について説明します。

ブートオプションを編集することで、次のことができます。

- デバッグを有効にして構成する

- 特定のカーネルまたはハードウェアアブストラクションレイヤー (HAL) ファイルを読み込む

- Windows で使用可能な物理メモリを制限する

- 32ビットバージョンの Windows での物理アドレス拡張 (PAE) の有効化、無効化、および構成

- ユーザーモードとカーネルモードのコンポーネント (3GB) の間で仮想アドレス空間を再分配し、非常に小さなカーネルモードのアドレス空間でドライバーをテストします。

- データ実行防止の有効化と構成 (/noexecute)

- ヘッドレスサーバーでの緊急管理サービス (EMS) コンソールのリダイレクトに使用するポートの指定

- ドライバーが読み込まれたときの名前の表示

このセクションの内容:

- [ブートオプションの概要](introduction-to-boot-options.md)
- [Windows のブートオプションの概要に](boot-options-in-windows.md)ついて説明します。
- [ブートオプション識別子](boot-options-identifiers.md)
- [ブートオプションの編集](editing-boot-options.md)
- [BCD ブートオプションのリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)
- [ブートパラメーターの使用](using-boot-parameters.md)
- [ブートオプションのバイパス](bypassing-boot-options.md)
- [BCD ブートオプションのリファレンス](bcd-boot-options-reference.md)
- [以前のバージョンの Windows でのブートオプション](boot-options-in-previous-versions-of-windows.md)

