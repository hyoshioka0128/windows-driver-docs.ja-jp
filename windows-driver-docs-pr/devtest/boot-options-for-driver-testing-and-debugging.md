---
title: ドライバーのテストとデバッグ用のブート オプション変更ツール
description: ドライバーのテストとデバッグ用のブート オプション変更ツール
ms.assetid: 4fd58868-7a43-42e3-adf9-5a82593c1675
keywords:
- ツールを WDK、ブート オプション
- ドライバーの開発ツールを WDK、ブート オプション
- WDK のブート オプション
- ドライバー WDK ブート オプションをテストします。
- テスト ドライバー WDK ブート オプション
- ドライバー WDK ブート オプションのデバッグ
- ドライバー WDK ブート オプションのデバッグ
- WDK のオペレーティング システムのブート オプション
- WDK のブート オプションの構成を読み込む
ms.date: 04/19/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6e08f97513d125f2bad0365a6475883e63338afd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360428"
---
# <a name="tools-for-changing-boot-options-for-driver-testing-and-debugging"></a>ドライバーのテストとデバッグ用のブート オプション変更ツール

テストして、Microsoft Windows オペレーティング システム上のドライバーをデバッグを有効にして、オペレーティング システムの読み込み時に確立されている機能を構成する必要があります。 これらの機能の設定が含まれている、*ブート オプション*--ブート ローダーの読み込みし、オペレーティング システムとその他の起動可能なプログラム、およびデバイスの構成を決定する値。


このセクションでは、追加、削除、およびオペレーティング システムの負荷の新しい構成を作成するためのブート オプションを変更する方法と、ブート エントリのパラメーターを使用して、ドライバーのテストとデバッグの構成をロードをカスタマイズする方法について説明します。

ブート オプションを編集するには、次の操作を実行できます。

- 有効にして、デバッグの構成

- 特定のカーネル、またはハードウェア アブストラクション レイヤー (HAL) ファイルを読み込む

- Windows で使用できる物理メモリを制限します。

- 有効化、無効にする、および 32 ビット バージョンの Windows の物理アドレス拡張 (PAE) を構成します。

- 非常に小さなカーネル モード アドレス空間でドライバーをテストする (3 GB) のユーザー モードとカーネル モード コンポーネント間の仮想アドレス空間を配分します。

- 有効にして構成データ実行防止 (/noexecute)

- ヘッドレス サーバーでコンソール リダイレクトを緊急管理サービス (EMS) 用のポートを指定します。

- 読み込まれるドライバーの名前を表示します。

このセクションの内容:

- [ブート オプションの概要](introduction-to-boot-options.md)
- [ブートの概要については、Windows でオプション](boot-options-in-windows.md)します。
- [ブート オプションの識別子](boot-options-identifiers.md)
- [ブート オプションの編集](editing-boot-options.md)
- [BCD のブート オプション リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)
- [ブート パラメーターを使用します。](using-boot-parameters.md)
- [バイパスのブート オプション](bypassing-boot-options.md)
- [BCD のブート オプション リファレンス](bcd-boot-options-reference.md)
- [以前のバージョンの Windows のブート オプション](boot-options-in-previous-versions-of-windows.md)

